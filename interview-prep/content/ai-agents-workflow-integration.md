# AI Agents & Workflow Integration

Interview question bank from `LLM_Azure_AI_Interview_700_QA.docx`.

## Questions

### 1. What is an AI agent?

**Answer:** An AI agent is an LLM-based system that can plan, use tools, remember context, and perform tasks.

### 2. How is an agent different from a chatbot?

**Answer:** A chatbot mainly responds; an agent can take steps, call tools, and work toward a goal.

### 3. What are tools in an AI agent?

**Answer:** Tools are external functions or APIs the agent can use, such as search, database, email, or calculator.

### 4. What is tool calling?

**Answer:** Tool calling is when the model chooses atool and passes structured arguments to it.

### 5. What is agent planning?

**Answer:** Planning means breaking a task into smaller steps before acting.

### 6. What is observe-act loop?

**Answer:** The agent acts, observes the result, anddecides the next action.

### 7. What is ReAct pattern?

**Answer:** ReAct combines reasoning and actions so the model can decide what tool to use and interpret results.

### 8. What is function schema?

**Answer:** It defines tool name, description, inputs, and data types so the model can call it correctly.

### 9. Why validate tool inputs?

**Answer:** Validation prevents wrong, unsafe, or malformed API calls.

### 10. What is workflow integration?

**Answer:** It connects an AI system with business systems like CRM, ticketing, email,databases, and approvals.

### 11. What is orchestration?

**Answer:** Orchestration coordinates multiple steps, tools, services, or agents in a controlled flow.

### 12. What is deterministic workflow?

**Answer:** A deterministic workflow follows fixed rulesand predictable paths.

### 13. What is agentic workflow?

**Answer:** An agentic workflow allows the model to decide some steps dynamically.

### 14. When should you avoid full autonomy?

**Answer:** Avoid it when actions are risky, costly, irreversible, or involve sensitive data.

### 15. What is human approval step?

**Answer:** A step where a person reviews and approves before the agent takes an important action.

### 16. What is HITL?

**Answer:** Human-in-the-loop means humans supervise, review, or approve AIdecisions/actions.

### 17. What is task decomposition?

**Answer:** Breaking a large goal into smaller tasks that are easier to solve.

### 18. What is a multi-agent system?

**Answer:** A system with multiple specialized agents collaborating on a task.

### 19. Why use multiple agents?

**Answer:** Different agents can specialize in research, coding, review, planning, ordomain tasks.

### 20. What is agent memory?

**Answer:** Memory stores past interactions, userpreferences, or task state for future use.

### 21. What is short-term memory?

**Answer:** Temporary context used during the current conversation or task.

### 22. What is long-term memory?

**Answer:** Information saved across sessions or tasks for future retrieval.

### 23. What is state management?

**Answer:** State management tracks progress, decisions, variables, and outputs acrossworkflow steps.

### 24. Why is state important in workflows?

**Answer:** Without state, the system may repeatwork, lose context, or make inconsistent decisions.

### 25. What is LangChain?

**Answer:** LangChain is a framework for building LLM apps with prompts, models, tools, memory, and retrieval.

### 26. What is LangGraph?

**Answer:** LangGraph builds stateful agent workflows as graphs with nodes, edges, and controlled execution.

### 27. Why use LangGraph for agents?

**Answer:** It makes agent steps more controllable, observable, and easier to recover from.

### 28. What is a node in workflow graph?

**Answer:** A node is one step or function in theworkflow.

### 29. What is an edge in workflow graph?

**Answer:** An edge defines where the workflow goes next.

### 30. What is conditional routing?

**Answer:** The workflow chooses the next step based on current state or model output.

### 31. What is retry policy?

**Answer:** Rules for repeating failed steps safely.

### 32. What is timeout?

**Answer:** A maximum waiting time before stopping a slow operation.

### 33. What is circuit breaker pattern?

**Answer:** It stops calling a failing service temporarily to prevent repeated failures.

### 34. What is idempotent action?

**Answer:** An action that can be repeated without changing the final result unexpectedly.

### 35. Why is idempotency important for agents?

**Answer:** Agents may retry actions, so idempotency prevents duplicate emails, tickets, orpayments.

### 36. What is event-driven workflow?

**Answer:** A workflow triggered by events like file upload, form submission, or message arrival.

### 37. What is scheduled workflow?

**Answer:** A workflow that runs at a fixed time or interval.

### 38. What is API-based integration?

**Answer:** Connecting systems through APIs to readdata or perform actions.

### 39. What is webhook?

**Answer:** A webhook sends data to your app when an event happens.

### 40. What is queue-based integration?

**Answer:** A system places tasks in a queue andworkers process them asynchronously.

### 41. Why use queues for agent workflows?

**Answer:** Queues improve reliability for long-running or high-volume tasks.

### 42. What is message broker?

**Answer:** A service that passes messages between systems, such as Service Bus or Kafka.

### 43. What is durable workflow?

**Answer:** A workflow that saves progress and canresume after failure.

### 44. What is compensation action?

**Answer:** A reverse or cleanup action when a previous step must be undone.

### 45. What is saga pattern?

**Answer:** A pattern for managing multi-step transactions using compensating actions.

### 46. What is observability in agents?

**Answer:** Tracking prompts, tool calls, latency,errors, decisions, and outputs.

### 47. Why trace agent steps?

**Answer:** Tracing helps debug why the agent made a decision or failed.

### 48. What should be logged in agent systems?

**Answer:** Log task ID, tool calls, errors, latency, and safe summaries, while protecting sensitive data.

### 49. What is prompt injection in agents?

**Answer:** A malicious instruction tries to trick theagent into ignoring rules or misusing tools.

### 50. Why are agents more vulnerable to prompt injection?

**Answer:** Because they can call tools and take actions, so bad instructions can cause real impact.

### 51. How do you secure agent tools?

**Answer:** Use allowlists, scoped permissions, input validation, human approval, and audit logs.

### 52. What is tool permission scoping?

**Answer:** Giving each tool only the minimumpermissions needed.

### 53. What is read-only tool?

**Answer:** A tool that can only fetch data and cannotchange anything.

### 54. What is write-action tool?

**Answer:** A tool that modifies data or performs actions like sending email or updating records.

### 55. When require approval for tools?

**Answer:** Require approval for external communication, financial actions, deletion, permissions, or sensitive updates.

### 56. What is grounding in agents?

**Answer:** Providing trusted data so the agent bases actions on real context.

### 57. What is agent evaluation?

**Answer:** Testing whether the agent completes tasks correctly, safely, and efficiently.

### 58. What is task success rate?

**Answer:** The percentage of tasks completedcorrectly.

### 59. What is tool-call accuracy?

**Answer:** How often the agent selects the right tool with correct arguments.

### 60. What is step-level evaluation?

**Answer:** Evaluating each intermediate action, notonly the final answer.

### 61. What is regression test for agents?

**Answer:** A saved test case used to ensure new changes do not break existing behavior.

### 62. What is sandbox environment?

**Answer:** A safe test environment where actions do not affect real users or production data.

### 63. Why test agents in sandbox first?

**Answer:** Because wrong actions can damage realsystems or data.

### 64. What is production monitoring?

**Answer:** Continuous tracking of live agent quality, cost, failures, and safety.

### 65. What is escalation?

**Answer:** Routing a task to a human when the agentis unsure or risk is high.

### 66. What is confidence score?

**Answer:** A score estimating how reliable the agent's answer or action is.

### 67. Why can confidence scores be tricky?

**Answer:** LLMs may sound confident even when wrong, so confidence should be validated.

### 68. What is fallback behavior?

**Answer:** A safe response path when the agentcannot complete a task.

### 69. What is MCP?

**Answer:** Model Context Protocol is a standard way for AI apps to connect to tools and data sources.

### 70. Why is MCP useful?

**Answer:** It can reduce custom integrations by providing a common tool/data connection pattern.

### 71. What is CRM integration?

**Answer:** Connecting the agent to customer data and actions in a CRM system.

### 72. What is ticketing integration?

**Answer:** Connecting the agent to tools like Jira, ServiceNow, or Zendesk to create orupdate tickets.

### 73. What is calendar integration?

**Answer:** Allowing the agent to check availability, schedule meetings, or send invites.

### 74. What is email integration risk?

**Answer:** The agent might send wrong, sensitive, orunauthorized messages if not controlled.

### 75. How do you design an agent for customer support?

**Answer:** Ground it on FAQs and policies, integrate ticket tools, add escalation, monitor quality, and restrict actions.

### 76. How do you design an agent for document processing?

**Answer:** Use OCR/extraction, validation, RAG, structured outputs, queue processing, and human review for low confidence.

### 77. What is structured output in workflows?

**Answer:** Model output formatted as JSON orschema-based data for the next system step.

### 78. Why is structured output important?

**Answer:** Workflows need predictable fields tocontinue processing automatically.

### 79. What is schema evolution?

**Answer:** Updating data schemas over time while keeping compatibility.

### 80. What is versioning in agent workflows?

**Answer:** Tracking prompt, tool, model, and workflow versions for testing and rollback.

### 81. Why version prompts?

**Answer:** Prompt changes can change behavior, soversions help debug and rollback.

### 82. What is model routing in workflows?

**Answer:** Choosing different models for different steps based on complexity, cost, or speed.

### 83. What is small-model first strategy?

**Answer:** Try a cheaper model first and use astronger model only when needed.

### 84. What is cost guardrail?

**Answer:** A limit or control to prevent the agent from spending too much on model/tool calls.

### 85. What is infinite loop risk?

**Answer:** The agent may keep repeating steps without finishing.

### 86. How do you prevent loops?

**Answer:** Set max steps, timeouts, stop rules, and repeated-action detection.

### 87. What is approval workflow?

**Answer:** A business process where specific usersapprove actions before completion.

### 88. How do agents fit Agile teams?

**Answer:** They can automate support, summarization, coding assistance, testing, and knowledge retrieval.

### 89. What is agent handoff?

**Answer:** One agent or system passes work to another agent or human.

### 90. What is role specialization?

**Answer:** Giving each agent a clear responsibility toreduce confusion.

### 91. What is least-authority agent design?

**Answer:** Give the agent only the tools and permissions needed for its task.

### 92. What is a safe agent architecture?

**Answer:** Use controlled tools, validated inputs, permission scopes, monitoring, human approval, and rollback plans.

### 93. How would you explain agent workflow to a client?

**Answer:** It is like an AI assistant that follows a controlled process, uses approved tools, and asks humans for approval whenneeded.

### 94. What is the biggest production challenge with agents?

**Answer:** Reliability: making sure the agent consistently takes correct, safe, and explainable actions.

### 95. What is an important interview point for AI Agents & Workflow Integration?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

### 96. What is an important interview point for AI Agents & Workflow Integration?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs orlimitations.

### 97. What is an important interview point for AI Agents & Workflow Integration?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

### 98. What is an important interview point for AI Agents & Workflow Integration?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

### 99. What is an important interview point for AI Agents & Workflow Integration?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

### 100. What is an important interview point for AI Agents & Workflow Integration?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs orlimitations.

