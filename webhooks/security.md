# Webhook Security

Every webhook request from Manus includes a cryptographic signature. Verifying it ensures the request is authentic and hasn't been tampered with.

## How It Works

Manus signs each request using **RSA-SHA256** (2048-bit key). Your server verifies the signature with our public key.

**Step 1 — Extract headers.** Read `X-Webhook-Signature` and `X-Webhook-Timestamp` from the incoming request.

**Step 2 — Check timestamp.** Reject requests older than 5 minutes to prevent replay attacks.

**Step 3 — Reconstruct the signed content.** Concatenate: `{timestamp}.{url}.{sha256_hex(body)}`

**Step 4 — Verify signature.** Hash the content with SHA-256, then verify the signature using the public key.

## Request Headers

| Header | Description |
|---|---|
| `X-Webhook-Signature` | Base64-encoded RSA-SHA256 signature |
| `X-Webhook-Timestamp` | Unix timestamp (seconds) of when the request was sent |

## Signature Format

The signature is computed over this string:

```
{timestamp}.{url}.{body_sha256_hex}
```

**Example:**
```
1704067200.https://api.yourapp.com/webhooks.a1b2c3d4e5f6...
```

## Get the Public Key

Fetch the public key from the [`webhook.publicKey`](../api-reference/webhooks/webhook.publicKey.md) endpoint:

```bash
curl 'https://api.manus.ai/v2/webhook.publicKey' \
  -H 'x-manus-api-key: YOUR_API_KEY'
```

```json
{
  "ok": true,
  "public_key": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQE...\n-----END PUBLIC KEY-----",
  "algorithm": "RSA-SHA256"
}
```

> **Performance tip:** Cache this key on your server with a reasonable TTL (e.g. 1 hour). Do not fetch it on every webhook request.

## Verification Examples

**Python:**
```python
import base64, hashlib, time
from cryptography.hazmat.primitives import hashes, serialization
from cryptography.hazmat.primitives.asymmetric import padding
from cryptography.exceptions import InvalidSignature

def verify_webhook(public_key_pem, url, body, signature_b64, timestamp):
    # 1. Check timestamp freshness (5-minute window)
    if abs(int(time.time()) - int(timestamp)) > 300:
        return False

    # 2. Reconstruct signed content
    body_hash = hashlib.sha256(body).hexdigest()
    signed_content = f"{timestamp}.{url}.{body_hash}".encode()

    # 3. Hash the content
    content_hash = hashlib.sha256(signed_content).digest()

    # 4. Verify signature
    try:
        key = serialization.load_pem_public_key(public_key_pem.encode())
        key.verify(
            base64.b64decode(signature_b64),
            content_hash,
            padding.PKCS1v15(),
            hashes.SHA256()
        )
        return True
    except (InvalidSignature, Exception):
        return False
```

**Flask handler:**
```python
@app.route("/webhooks", methods=["POST"])
def handle_webhook():
    sig = request.headers.get("X-Webhook-Signature")
    ts = request.headers.get("X-Webhook-Timestamp")

    if not sig or not ts:
        return "Missing headers", 400

    if not verify_webhook(get_cached_public_key(), request.url, request.data, sig, ts):
        return "Unauthorized", 401

    # Process webhook
    data = request.json
    process_event(data)
    return "OK", 200
```

**Node.js:**
```javascript
const crypto = require('crypto');

function verifyWebhook(publicKeyPem, url, body, signatureB64, timestamp) {
  // 1. Check timestamp freshness (5-minute window)
  if (Math.abs(Date.now() / 1000 - parseInt(timestamp)) > 300) {
    return false;
  }

  // 2. Reconstruct signed content
  const bodyHash = crypto.createHash('sha256').update(body).digest('hex');
  const signedContent = `${timestamp}.${url}.${bodyHash}`;

  // 3. Hash the content
  const contentHash = crypto.createHash('sha256').update(signedContent).digest();

  // 4. Verify signature
  try {
    const verify = crypto.createVerify('RSA-SHA256');
    verify.update(contentHash);
    return verify.verify(publicKeyPem, signatureB64, 'base64');
  } catch {
    return false;
  }
}
```

## Best Practices

**Always verify signatures** before processing any webhook payload to prevent spoofed requests.

**Reject stale timestamps** — the 5-minute window protects against replay attacks.

**Cache the public key** with a TTL of at least 1 hour to avoid unnecessary API calls on every webhook.

**Return `200` quickly** — process webhooks asynchronously if needed. Manus expects a response within 10 seconds.

**Use HTTPS** — never expose a webhook endpoint over plain HTTP.
