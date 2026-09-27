# Adaptive interview question bank

Use this as a branching checklist. Resolve 30–100 meaningful decisions based on complexity. Do not ask irrelevant questions or repeat facts already supplied by the user.

## A. Outcome and scope
1. What exact outcome should exist when the project is finished?
2. Who is the primary operator/user?
3. What problem is it replacing or improving?
4. What is explicitly out of scope?
5. What does a successful end-to-end run look like?
6. What would make the project a failure even if it technically runs?
7. Is this a prototype, internal tool, production service, or customer-facing system?
8. Is there an existing project/repository to extend?

## B. Inputs and triggers
9. What starts the workflow: user message, email, webhook, schedule, file, queue, API call, or something else?
10. Which input channels are mandatory at launch?
11. What input formats must be accepted?
12. What invalid/malformed inputs must be rejected or quarantined?
13. Are historical items processed or only new items?
14. Is deduplication/idempotency required?
15. What expected input volume and burst volume should be supported?

## C. Outputs and actions
16. What must the system produce or change?
17. Which actions are read-only versus write/destructive?
18. Which actions require human approval before execution?
19. Which actions can be fully autonomous?
20. What output formats are required?
21. Who/what receives each output?
22. Must actions be reversible or compensatable?

## D. Data and state
23. What is the system of record?
24. Which entities/records exist?
25. What identifiers uniquely identify them?
26. What state must survive restarts?
27. What retention period is required?
28. What data must never be stored?
29. Is a database required? If yes, which one is preferred/already available?
30. Is full-text/vector retrieval needed or only structured lookup?
31. Are migrations/seed data needed?
32. What concurrency or locking concerns exist?

## E. Integrations and credentials
33. Which external services/APIs are required?
34. Which are already configured?
35. Are MCP servers involved?
36. Which integration operations are read versus write?
37. What auth method does each service use?
38. Where should secrets be stored?
39. What rate limits/quotas matter?
40. What should happen when an integration is unavailable?
41. Is there a sandbox/test environment for each write integration?

## F. Hermes execution model
42. Where will Hermes run: desktop, local CLI, VPS, container, messaging surface, or other documented surface?
43. Will Hermes have terminal/file access to the project?
44. Which documented Hermes toolsets/features are expected to be available?
45. Are custom skills needed inside Hermes?
46. Are MCP integrations expected inside Hermes?
47. Are subagents/delegation required or optional?
48. Does the workflow need scheduled/background execution?
49. Must Hermes resume/recover sessions after interruption?
50. Are there environment-specific restrictions that Hermes must respect?

## G. AI behavior
51. What decisions should the model make?
52. What decisions must never be delegated to the model?
53. Is structured JSON/output schema required?
54. What confidence/uncertainty behavior is expected?
55. What information may the model infer versus only retrieve?
56. What hallucination-sensitive fields require source grounding?
57. What tone/persona is required for generated communication?
58. Is multilingual behavior required?
59. What escalation conditions require a human?

## H. Safety, privacy, permissions
60. What sensitive data is handled?
61. What access-control roles exist?
62. What audit trail is required?
63. Which operations could cause financial/legal/customer impact?
64. What confirmation gates are required?
65. What must be redacted from logs?
66. What data residency/compliance constraints exist?
67. What prompt-injection/untrusted-content risks exist?

## I. Reliability and errors
68. Which failures are retryable?
69. What retry/backoff policy is acceptable?
70. What failures should stop one item versus the whole pipeline?
71. What happens to partially completed work?
72. How are poison/bad inputs quarantined?
73. What timeout limits matter?
74. What manual recovery procedure is acceptable?
75. What health checks are required?

## J. UI, reporting, observability
76. Is a UI/dashboard required?
77. Which KPIs/statuses must be visible?
78. What filters/search/detail views are needed?
79. What logs should operators see?
80. Are notifications/alerts required?
81. Where should alerts go?
82. Is CSV/export/reporting required?
83. What should be inspectable for each processed item?

## K. Deployment and operations
84. What OS/runtime/environment will host the project?
85. What startup/restart mechanism is preferred?
86. Must the service survive reboot?
87. Is Docker required, optional, or unwanted?
88. What ports/domains/network restrictions exist?
89. How are updates deployed?
90. What backup strategy is required?
91. What rollback strategy is required?
92. Who will operate it day to day?

## L. Testing and acceptance
93. What test data/fixtures are available?
94. Which happy-path scenarios must pass?
95. Which failure/edge scenarios must pass?
96. What external integrations can be safely tested live?
97. What needs mocks/sandbox tests instead?
98. What is the final acceptance checklist?
99. What evidence should Hermes report after each step?
100. What exact production verification proves the project is complete?
