# Microsoft Azure AI Foundry

Interview question bank from `LLM_Azure_AI_Interview_700_QA.docx`.

## Questions

### 1. What is Microsoft Azure AI Foundry?

**Answer:** It is Microsoft's platform for building, evaluating, deploying, and governing AI apps and agents.

### 2. Why use Azure AI Foundry?

**Answer:** It brings models, tools, evaluation, safety, deployment, and governance into one Azure-based development platform.

### 3. What is Foundry Models?

**Answer:** It is a model catalog where developers can discover and use foundation models from multiple providers.

### 4. What kinds of models are available in Foundry?

**Answer:** Text, chat, reasoning, vision, embedding, audio, and other foundation modelsdepending on region and availability.

### 5. What is model catalog?

**Answer:** A place to browse models, compare capabilities, and deploy selected models.

### 6. What is model deployment?

**Answer:** Making a selected model available throughan endpoint or API.

### 7. What is endpoint in Foundry/Azure AI?

**Answer:** An endpoint is the URL/API target used by applications to call a deployed model.

### 8. What is deployment name?

**Answer:** It is the name assigned to a modeldeployment and used in API requests.

### 9. What is Foundry Agent Service?

**Answer:** It is a managed service for building, deploying, and scaling AI agents.

### 10. What is a prompt agent?

**Answer:** A no-code or low-code agent configured with instructions, models, tools, andknowledge.

### 11. What is a code-based hosted agent?

**Answer:** An agent built with code or frameworks and hosted/managed through Foundry capabilities.

### 12. What frameworks can integrate with Foundry Agent Service?

**Answer:** Frameworks such as LangGraph or custom code can be used depending on supported SDKs and service options.

### 13. What is grounding in Foundry?

**Answer:** Connecting models or agents to trusted enterprise knowledge sources.

### 14. What knowledge sources can agents use?

**Answer:** Examples include search indexes, enterprise documents, SharePoint, Fabric, Bing, or custom data sources dependingon setup.

### 15. What are action connectors?

**Answer:** Connectors let agents perform actions in external business systems.

### 16. Why are connectors useful?

**Answer:** They help agents move from answering questions to completing business tasks.

### 17. What is Azure AI Search's role inFoundry?

**Answer:** It can provide keyword, vector, and hybridretrieval for RAG apps.

### 18. What is RAG in Foundry?

**Answer:** A pattern where Foundry apps retrieve enterprise data and pass it to a model for grounded answers.

### 19. What is evaluation in Foundry?

**Answer:** Evaluation measures model/app quality such as relevance, groundedness, safety, and performance.

### 20. Why evaluate AI apps before production?

**Answer:** Because AI outputs can vary, and evaluation catches quality, safety, andgrounding issues.

### 21. What is responsible AI?

**Answer:** Responsible AI means building AI that is safe, fair, transparent, secure, and accountable.

### 22. What is content safety?

**Answer:** Content safety detects or blocks harmful orinappropriate input/output.

### 23. What is prompt shield or prompt protection?

**Answer:** A safety layer that helps defend against prompt injection or malicious instructions.

### 24. What is model monitoring?

**Answer:** Tracking quality, performance, cost, errors, and safety after deployment.

### 25. What is tracing in AI Foundry apps?

**Answer:** Tracing records execution steps such as prompts, model calls, and tool calls for debugging.

### 26. Why is tracing important for agents?

**Answer:** It explains what happened when an agent made a decision or failed.

### 27. What is governance in Foundry?

**Answer:** Policies and controls for model usage, data access, safety, monitoring, and compliance.

### 28. What is enterprise security in Foundry?

**Answer:** Using Azure identity, networking, RBAC, private access, and audit controls tosecure AI apps.

### 29. What is RBAC in Azure Foundry context?

**Answer:** It controls who can view, deploy, manage, or call AI resources.

### 30. What is managed identity with Foundry?

**Answer:** It lets apps access Azure resourceswithout storing credentials.

### 31. What is private networking?

**Answer:** Keeping traffic inside private Azure networks instead of the public internet.

### 32. Why use private endpoints?

**Answer:** They reduce exposure by allowing private access to Azure services.

### 33. What is data residency?

**Answer:** Keeping data in required geographicregions for compliance or policy reasons.

### 34. Why check regional availability?

**Answer:** Not every model or feature is available in every Azure region.

### 35. What is quota in Azure AI services?

**Answer:** Quota limits how much capacity, tokens, or requests you can use.

### 36. What is rate limit?

**Answer:** A limit on number of requests or tokens ina time window.

### 37. How do you handle rate limits?

**Answer:** Use retries with backoff, queues, capacity planning, and request optimization.

### 38. What is model selection?

**Answer:** Choosing the best model for task quality,cost, speed, and compliance needs.

### 39. How choose between large and small models?

**Answer:** Use large models for complex reasoning and smaller models for high-volume simple tasks.

### 40. What is cost management in Foundry?

**Answer:** Tracking model usage, tokens, deployments, and infrastructure to controlspending.

### 41. How reduce cost in Foundry apps?

**Answer:** Use efficient prompts, caching, smaller models, batching, retrieval filtering, and usage limits.

### 42. What is prompt flow?

**Answer:** A workflow approach for designing, testing, and evaluating prompt/model pipelines.

### 43. Why use prompt flow?

**Answer:** It helps organize prompts, tools, datasets,tests, and evaluations.

### 44. What is AI project lifecycle?

**Answer:** Plan, prototype, evaluate, secure, deploy, monitor, and improve.

### 45. What is model benchmarking?

**Answer:** Comparing models on the same tasks tochoose the best one.

### 46. What is safety evaluation?

**Answer:** Testing whether the app avoids harmful, biased, or unsafe outputs.

### 47. What is groundedness metric?

**Answer:** It checks whether answers are supportedby provided source data.

### 48. What is relevance metric?

**Answer:** It checks whether the answer is useful and related to the question.

### 49. What is coherence metric?

**Answer:** It checks whether the response is clearand logically organized.

### 50. What is fluency metric?

**Answer:** It checks grammar, readability, and natural language quality.

### 51. What is latency metric?

**Answer:** It measures how long the app takes to respond.

### 52. What is throughput?

**Answer:** The number of requests the system canprocess in a time period.

### 53. What is SLA consideration?

**Answer:** Expected service availability and performance commitments for production apps.

### 54. What is deployment slot or staging environment?

**Answer:** A separate environment to test changes before production rollout.

### 55. What is blue-green deployment for AI apps?

**Answer:** Run old and new versions separately, then switch traffic after validation.

### 56. What is canary release for AI apps?

**Answer:** Release to a small group first to monitor quality and risk.

### 57. What is rollback?

**Answer:** Returning to a previous stable version afterissues.

### 58. Why version prompts and models?

**Answer:** Because even small changes can affect output quality and behavior.

### 59. What is dataset in evaluation?

**Answer:** A collection of test inputs and expected outcomes used to measure app quality.

### 60. What is golden dataset?

**Answer:** A trusted set of representative examples used for repeatable evaluation.

### 61. What is A/B testing in AI apps?

**Answer:** Comparing two versions with real or testtraffic to see which performs better.

### 62. What is human review in Foundry workflows?

**Answer:** People evaluate outputs or approve risky actions before release or execution.

### 63. What is fine-tuning in Azure/Foundry?

**Answer:** Training a supported base model further on custom examples for a specific task.

### 64. When use fine-tuning in Foundry?

**Answer:** Use it when you need consistent style, format, or task behavior not solved byprompting/RAG.

### 65. When avoid fine-tuning?

**Answer:** Avoid it for frequently changing facts; use RAG instead.

### 66. What is embedding model?

**Answer:** A model that converts text into vectors for semantic search and similarity.

### 67. What is image generation model?

**Answer:** A model that creates images from text orother inputs.

### 68. What is audio model?

**Answer:** A model for speech-to-text, text-to-speech, translation, or real-time voice interactions.

### 69. What is multimodal model?

**Answer:** A model that handles multiple input types such as text, images, or audio.

### 70. What is SDK usage in Foundry?

**Answer:** Developers use SDKs to create clients,call models, manage agents, and integrate apps.

### 71. What is REST API usage?

**Answer:** Applications call model or agent endpointsusing HTTP requests.

### 72. What is authentication for Foundry APIs?

**Answer:** Use API keys, Azure identity, ortoken-based auth depending on service configuration.

### 73. Why use Azure identity over keys?

**Answer:** Identity-based auth is easier to rotate,audit, and secure.

### 74. What is key rotation?

**Answer:** Replacing old secrets/keys with new ones to reduce risk.

### 75. What is audit log?

**Answer:** A record of who did what and when in the system.

### 76. What is compliance need in enterprise AI?

**Answer:** Meeting rules for privacy, security, datahandling, and industry regulations.

### 77. What is data grounding with enterprise documents?

**Answer:** Indexing company documents and retrieving relevant pieces for model answers.

### 78. How would you build enterprise Q&A in Foundry?

**Answer:** Use document ingestion, Azure AI Search, model deployment, evaluation, content safety, RBAC, and monitoring.

### 79. How would you build an HR policy bot?

**Answer:** Ground it on approved HR documents, cite sources, restrict access by role, and escalate sensitive cases.

### 80. How would you build a customer support agent?

**Answer:** Connect knowledge base, CRM/ticket tools, add approval for account changes,and track resolution quality.

### 81. What is tool governance?

**Answer:** Controlling which tools agents can use, with what permissions, and under what conditions.

### 82. What is BYOD or bring your own data?

**Answer:** Using your organization's data sources toground AI responses.

### 83. What is BYOC or custom model scenario?

**Answer:** Using or deploying a model chosen/customized for business needs, where supported.

### 84. What is AI Foundry portal?

**Answer:** A web experience for creating projects, exploring models, building agents, and managing AI assets.

### 85. What is production readiness checklist?

**Answer:** Security, evaluation, monitoring, cost controls, fallback, documentation, and support process.

### 86. What is common interview question on Foundry?

**Answer:** They may ask how you would use Foundry to build a secure RAG chatbot or agent.

### 87. How answer that question simply?

**Answer:** I would select a model, connect enterprise data through search, evaluate outputs, addsafety, deploy API, and monitor usage.

### 88. What is the difference between Copilot Studio and Foundry Agent Service?

**Answer:** Copilot Studio is more low-code; Foundry Agent Service is more pro-code and flexible for complex enterprise agents.

### 89. What is agent observability in Foundry?

**Answer:** It means seeing model calls, tool calls, traces, latency, and errors for debuggingand governance.

### 90. What is secure memory for agents?

**Answer:** Memory stored with proper access control, privacy, encryption, and lifecycle management.

### 91. What is model lifecycle management?

**Answer:** Managing model selection, deployment, evaluation, monitoring, updates, and retirement.

### 92. What is a common mistake in Foundry projects?

**Answer:** Jumping to model calls before definingbusiness scope, data access, evaluation, and safety.

### 93. How would you explain Foundry to a non-technical manager?

**Answer:** It is a secure Microsoft platform to build and manage AI apps and agents usingcompany data and approved models.

### 94. What should you mention in an interview about Foundry?

**Answer:** Mention model catalog, agents, RAG, evaluation, safety, security, monitoring, and enterprise integration.

### 95. What is the key benefit of Foundry for enterprises?

**Answer:** It helps move AI solutions from prototype to governed, secure, scalable production.

### 96. What is an important interview point for Microsoft Azure AI Foundry?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

### 97. What is an important interview point for Microsoft Azure AI Foundry?

**Answer:** Explain the concept simply, give a practicalexample, and mention trade-offs or limitations.

### 98. What is an important interview point for Microsoft Azure AI Foundry?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs orlimitations.

### 99. What is an important interview point for Microsoft Azure AI Foundry?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

### 100. What is an important interview point for Microsoft Azure AI Foundry?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

