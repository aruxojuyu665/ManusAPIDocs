Skip to main content
8	Manus API home page
9	Search...
10	Ctrl K
11	Getting Started
12	Introduction
13	Authentication
14	Task Lifecycle
15	Connectors
16	Webhooks Guide
17	Agents
18	Integrations
19	Data Integrations
20	Website
21	Rate Limits
22	API Reference
23	Tasks
24	Projects
25	Skills
26	Agents
27	Files
28	Webhooks
29	Usage
30	Connectors
31	Browser
32	Website
33	GET
34	website.status
35	GET
36	website.listCheckpoints
37	POST
38	website.publish
39	POST
40	website.update
41	v2
42	Website
43	website.publish
44	Copy page
45	
46	Deploys the latest checkpoint of a website and sets its visibility. Deployment is asynchronous — poll website.status until publish_status becomes published or failed. To change metadata (title, visibility) without redeploying, use website.update instead. See the Website guide.
47	
48	POST
49	/
50	v2
51	/
52	website.publish
53	Try it
54	Questions or issues? Contact us at api-support@manus.ai.
55	Deploys latest: Always deploys the website’s most recent checkpoint — there is no version_id parameter. Use website.listCheckpoints to inspect history.
56	Asynchronous: Poll website.status until publish_status is published or failed.
57	Metadata-only change? To change title or visibility without redeploying, use website.update instead. See the Website guide.
58	Authorizations
59	​
60	x-manus-api-key
61	stringheaderrequired
62	Body
63	application/json
64	​
65	task_id
66	string
67	
68	Session UID. Mutually exclusive with website_id — exactly one must be provided.
69	
70	​
71	website_id
72	string
73	
74	Unique website ID. Mutually exclusive with task_id — exactly one must be provided.
75	
76	​
77	visibility
78	enum<string>
79	
80	Who can access the published site. Defaults to public when omitted or sent as empty string. team is only available to team accounts. Sites may cap the maximum allowed visibility — requests that exceed it return 403 permission_denied.
81	
82	Available options: public, team 
83	Response
84	200
85	application/json
86	
87	Publish triggered successfully. Deployment is still in progress — poll website.status for the final state.
88	
89	​
90	ok
91	boolean
92	
93	Whether the request was successful.
94	
95	Example:
96	
97	true
98	
99	​
100	request_id
101	string
102	
103	Unique identifier for this API request.
104	
105	​
106	website_id
107	string
108	
109	Unique website ID.
110	
111	​
112	version_id
113	string
114	
115	version_id of the checkpoint being deployed — always the latest checkpoint of the site.
116	
117