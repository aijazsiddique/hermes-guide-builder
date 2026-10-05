# Adaptive Question Bank — Octop Multi-Agent Systems

Do not ask all questions. Select only questions whose answers can change the design. Reuse user-provided facts.

## A. Outcome and scope
1. What exact outcome should this agent system deliver?
2. What is the first real-world workflow it must handle end to end?
3. What would make you say the system is successful after one week?
4. What is explicitly out of scope for v1?
5. Is this personal, internal-team, client-facing, or public-facing?
6. Is the goal speed, accuracy, cost, autonomy, auditability, or a ranked combination?
7. What must never happen even if it reduces automation?
8. Is there a hard delivery/deployment deadline?

## B. User interaction and entry point
9. Where will the human primarily talk to the system: Octop Dashboard, Telegram, Discord, Feishu, another channel, API, or several?
10. Should users see a single team conversation or interact with specialists individually?
11. Should specialist messages be visible directly, or should one coordinator synthesize everything?
12. Will users `@` specific experts?
13. Should the system ask clarifying questions before acting, or default aggressively?
14. Are there different user roles with different permissions?
15. Does the system need multilingual interaction?
16. Is the coordinator allowed to give short direct answers for greetings/clarifications?

## C. Topology
17. Must the coordinator itself browse, code, run shell commands, edit files, or use Connectors/MCP?
18. Are there at least two genuinely distinct specialist roles?
19. Can specialist work run in parallel?
20. Is synchronous specialist consultation needed for some decisions?
21. Do specialists need to call each other directly?
22. Is a native group/team room important enough to accept a coordinator-only host?
23. Would one powerful expert plus subagents/tools be simpler?
24. Is a hybrid topology justified by a concrete workflow boundary?

## D. Agent roster and responsibilities
25. What specialist roles do you already know you need?
26. For each role, what inputs does it receive?
27. What exact output does each role produce?
28. What decisions is each role authorized to make independently?
29. What decisions require another agent’s approval?
30. What decisions require human approval?
31. Which role owns final quality control?
32. Which role handles failures/retries?
33. Which role communicates externally?
34. Which role, if any, may perform destructive operations?
35. Are any roles temporary rather than persistent experts?
36. Do any existing Octop experts already cover these roles and need to be reused?

## E. Models and cost
37. Is a specific model required for any role, or should the guide select from models actually configured in the instance?
38. Which tasks need strongest reasoning vs cheapest/fastest execution?
39. Are vision/audio/media capabilities required?
40. Is there a per-task, daily, or monthly model-cost ceiling?
41. Can a role fall back to another model if its preferred model is unavailable?
42. Do you need different models per specialist?

## F. Tools and execution surfaces
43. Which agents need filesystem read/write?
44. Which agents need shell execution?
45. Which agents need web fetch/search?
46. Which agents need interactive browser control?
47. Which agents need desktop/mobile control?
48. Which agents need image/video generation?
49. Which agents need ACP coding delegation (Codex/OpenCode/Claude Code/etc.)?
50. Are there tools a role must explicitly NOT receive?
51. Are least-privilege tool settings important for this deployment?

## G. Skills and durable policy
52. What reusable operating rules should live in a Skill instead of a one-off prompt?
53. Do you already have Skills to install/reuse?
54. Should each specialist have a role-specific Skill?
55. Are there hard numerical/business rules that must be stored once and referenced consistently?
56. Should shared packet schemas live in a reference file/Skill?
57. How should Skill updates be reviewed and rolled out?

## H. MCP / Connectors / external systems
58. Which external apps/services must each role access?
59. Are those already configured as Octop Connectors/MCP servers?
60. Does any role need write/action permissions rather than read-only access?
61. What credentials/auth flows require a human setup step?
62. What should happen when an external service is unavailable or rate-limited?
63. Are there data residency or privacy constraints on connector use?
64. Does any integration need webhook/event-driven behavior outside ordinary chat?

## I. Knowledge and files
65. What reference documents/knowledge bases must each role use?
66. Can all roles see the same knowledge, or must it be isolated?
67. Are source citations/provenance required in answers?
68. Where should generated files live?
69. Should artifacts be passed in assignments, referenced by path, or uploaded to a shared external store?
70. What is the policy for temporary vs durable files?

## J. Memory and state
71. What should each agent remember across sessions?
72. What must never be stored in memory?
73. Is team-level memory separate from specialist memory?
74. Where do counters, queues, job IDs, dedupe keys, or workflow state live?
75. Does state need to survive Octop/server restart?
76. If an in-flight delegated task is lost on restart, what recovery behavior is required?
77. How should stale facts be expired or refreshed?

## K. Handoffs and packet contracts
78. Which agent-to-agent handoffs need a strict schema?
79. What fields are mandatory in each handoff?
80. How should confidence/uncertainty be represented?
81. What should a receiving agent do when required fields are missing?
82. Should a coordinator forward raw user text or create role-specific rewritten assignments?
83. What evidence should travel with a decision?

## L. Scheduling and proactive work
84. Are there recurring tasks?
85. Which agent should own each scheduled task?
86. What cadence/timezone matters?
87. Should scheduled jobs use a fresh thread or retained context?
88. What should happen when a scheduled run fails?
89. Should the system notify only on changes/conditions, or on every run?

## M. Safety, approvals, and audit
90. Which operations are financially, legally, security, privacy, or business consequential?
91. Which exact actions require a human confirmation immediately before execution?
92. Is there a spend/connect/quota/rate limit the agents must enforce?
93. Do you need an audit log of decisions and actions?
94. What secrets may agents read, and what secrets must never appear in output/logs?
95. What is the emergency stop/disable procedure?

## N. Testing and operations
96. What are the three most important happy-path acceptance scenarios?
97. What failure scenarios must be tested before activation?
98. What observable evidence proves routing and permissions are correct?
99. How should updates to Octop or the agent configuration be regression-tested?
100. What final status should mean “production ready,” and who gives the activation approval?

## Interview completion rule

Stop asking when all architecture-changing choices are resolved or explicitly deferred to a preflight step. Never force the user through all 100 questions just because they exist.