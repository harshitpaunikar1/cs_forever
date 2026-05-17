# Python on Azure

Interview question bank from `LLM_Azure_AI_Interview_700_QA.docx`.

## Questions

### 1. Why is Python commonly used for AI on Azure?

**Answer:** Python has strong AI libraries and Azure provides SDKs, compute, storage, and deployment services for it.

### 2. What is Azure SDK for Python?

**Answer:** It is a set of Python packages used to interact with Azure services programmatically.

### 3. How do you authenticate Python apps on Azure?

**Answer:** Use managed identity, service principal,Azure CLI credentials, or environment-based credentials.

### 4. What is DefaultAzureCredential?

**Answer:** It is an Azure Identity helper that tries common authentication methods in a safeorder.

### 5. What is managed identity?

**Answer:** Managed identity gives an Azure resource an identity so it can access other Azure services without storing secrets.

### 6. Why avoid hardcoding secrets in Pythoncode?

**Answer:** Hardcoded secrets can leak through Git,logs, screenshots, or deployments.

### 7. What is Azure Key Vault?

**Answer:** Key Vault securely stores secrets, keys, and certificates used by applications.

### 8. How do you read secrets from Key Vault in Python?

**Answer:** Use Azure Identity for auth and the Key Vault Secrets client to fetch secret values.

### 9. What is Azure Blob Storage?

**Answer:** Blob Storage stores files such as documents, images, logs, model outputs,and datasets.

### 10. How can Python upload a file to Blob Storage?

**Answer:** Use azure-storage-blob, create a BlobClient, and call upload_blob.

### 11. What is Azure Functions?

**Answer:** Azure Functions runs small pieces of codeon events without managing servers.

### 12. When use Azure Functions for AI apps?

**Answer:** Use it for lightweight triggers like file upload processing, webhook handling, or scheduled jobs.

### 13. What is Azure App Service?

**Answer:** App Service hosts web apps and APIs without managing virtual machines.

### 14. When use App Service over Functions?

**Answer:** Use App Service for long-running web APIs, web apps, and predictable HTTP services.

### 15. What is Azure Container Apps?

**Answer:** It runs containerized apps with scaling,revisions, and serverless-like operations.

### 16. When use containers for Python apps?

**Answer:** Use containers when you need consistent dependencies, custom runtimes, or portable deployment.

### 17. What is Docker?

**Answer:** Docker packages code and dependencies into a container image that runs consistently across environments.

### 18. What is Azure Container Registry?

**Answer:** ACR stores container images privately inAzure.

### 19. What is Azure Kubernetes Service?

**Answer:** AKS is managed Kubernetes for deploying and scaling containerized applications.

### 20. When use AKS?

**Answer:** Use AKS for complex microservices, advanced scaling, networking, and orchestration needs.

### 21. What is Azure Machine Learning?

**Answer:** Azure ML helps train, track, manage, anddeploy machine learning models.

### 22. What is a compute instance in Azure ML?

**Answer:** It is a cloud development machine for notebooks, experiments, and coding.

### 23. What is a compute cluster in Azure ML?

**Answer:** It is scalable compute used for training or batch jobs.

### 24. What is an Azure ML workspace?

**Answer:** It is the central place for ML assets such as datasets, jobs, models, environments, and endpoints.

### 25. What is an Azure ML environment?

**Answer:** It defines Python packages, Docker image, and runtime dependencies for jobs anddeployments.

### 26. Why use requirements.txt?

**Answer:** It records Python package dependencies so environments can be recreated.

### 27. Why use virtual environments?

**Answer:** They isolate package versions so one project does not break another.

### 28. What is pip?

**Answer:** pip installs Python packages from packageindexes or local files.

### 29. What is conda?

**Answer:** conda manages Python environments and packages, often useful for data science dependencies.

### 30. What is FastAPI?

**Answer:** FastAPI is a Python framework for building fast REST APIs with automatic validation and docs.

### 31. Why use FastAPI for LLM apps?

**Answer:** It is simple, async-friendly, supports typed request models, and works well for API services.

### 32. What is Flask?

**Answer:** Flask is a lightweight Python webframework for APIs and web apps.

### 33. FastAPI vs Flask?

**Answer:** FastAPI has built-in type validation and async support; Flask is simpler and very flexible.

### 34. What is async Python?

**Answer:** Async Python allows handling I/O taskswithout blocking the whole program.

### 35. Why is async useful for LLM APIs?

**Answer:** LLM apps wait on network calls, so async improves concurrency and responsiveness.

### 36. What is aiohttp/httpx?

**Answer:** They are Python libraries for making HTTP requests, with async support.

### 37. What is retry logic?

**Answer:** Retry logic repeats failed requests for temporary errors like rate limits or networkfailures.

### 38. What is exponential backoff?

**Answer:** It waits longer after each failed retry toavoid overwhelming a service.

### 39. What is logging in Python?

**Answer:** Logging records events, errors, and debugging information from an application.

### 40. What should you avoid logging in AI apps?

**Answer:** Avoid secrets, tokens, PII, confidentialprompts, and private documents unless properly protected.

### 41. What is Azure Monitor?

**Answer:** Azure Monitor collects logs and metrics to observe application and infrastructurehealth.

### 42. What is Application Insights?

**Answer:** Application Insights monitors app performance, requests, exceptions, traces, and dependencies.

### 43. What is OpenTelemetry?

**Answer:** OpenTelemetry is a standard for traces, metrics, and logs across services.

### 44. What is CI/CD?

**Answer:** CI/CD automates testing, building, and deployment of code changes.

### 45. How can Python apps be deployed to Azure?

**Answer:** Use App Service, Functions, Container Apps, AKS, Azure ML endpoints, orVM-based deployment.

### 46. What is GitHub Actions?

**Answer:** GitHub Actions automates workflows such as tests, builds, and Azure deployment.

### 47. What is Azure DevOps Pipelines?

**Answer:** It is Microsoft's CI/CD service for building, testing, and deploying applications.

### 48. What is infrastructure as code?

**Answer:** It defines cloud resources using code soenvironments are repeatable.

### 49. What is Bicep?

**Answer:** Bicep is an Azure language for defining infrastructure resources.

### 50. What is Terraform?

**Answer:** Terraform is an infrastructure-as-code tool used across cloud providers.

### 51. What is Azure Resource Group?

**Answer:** It is a logical container for Azureresources.

### 52. What is region in Azure?

**Answer:** A region is a geographic Azure data center area where resources run.

### 53. Why does region matter?

**Answer:** Region affects latency, availability, dataresidency, and supported services.

### 54. What is Azure RBAC?

**Answer:** Role-Based Access Control grants users or identities specific permissions on Azure resources.

### 55. What is least privilege?

**Answer:** Give only the permissions needed to perform a task, nothing extra.

### 56. What is Azure Virtual Network?

**Answer:** A VNet is a private network in Azure for secure resource communication.

### 57. What is private endpoint?

**Answer:** A private endpoint lets services be accessed privately inside a VNet instead ofpublic internet.

### 58. What is API Management?

**Answer:** Azure API Management secures, publishes, monitors, and manages APIs.

### 59. Why use API Management for LLM APIs?

**Answer:** It provides authentication, throttling, monitoring, versioning, and governance.

### 60. What is Azure Service Bus?

**Answer:** Service Bus is a messaging service forreliable communication between systems.

### 61. When use queues in AI apps?

**Answer:** Use queues for background processing, document ingestion, and tasks that may take time.

### 62. What is Event Grid?

**Answer:** Event Grid routes events from Azure services to handlers like Functions.

### 63. What is Azure Data Factory?

**Answer:** ADF builds data pipelines to move andtransform data.

### 64. What is Azure SQL Database?

**Answer:** It is a managed relational database servicein Azure.

### 65. What is Cosmos DB?

**Answer:** Cosmos DB is a globally distributed NoSQL database service.

### 66. When use Cosmos DB in AI apps?

**Answer:** Use it for chat history, metadata, userstate, and low-latency document records.

### 67. What is Azure AI Search?

**Answer:** It is a search service supporting keyword, vector, and hybrid search for RAG.

### 68. How does Python connect to Azure AI Search?

**Answer:** Use the Azure Search Documents SDK to upload documents, create indexes, and query results.

### 69. What is vector search in Azure AI Search?

**Answer:** It searches embeddings to findsemantically similar content.

### 70. What is hybrid search?

**Answer:** Hybrid search combines keyword search and vector search for better retrieval.

### 71. What is semantic ranking?

**Answer:** Semantic ranking improves search result order using language understanding.

### 72. What is Azure OpenAI?

**Answer:** Azure OpenAI provides access to OpenAI models through Azure security, networking, and compliance features.

### 73. How do you call an LLM from Python on Azure?

**Answer:** Use the appropriate SDK or REST API, pass messages/prompt, modeldeployment, and parameters.

### 74. What is deployment name in Azure OpenAI?

**Answer:** It is the custom name you give to a deployed model and use in API calls.

### 75. What is token limit error?

**Answer:** It happens when prompt plus response exceed the model's allowed context or output limits.

### 76. How do you handle token limits?

**Answer:** Chunk, summarize, retrieve only relevantdata, and limit response length.

### 77. What is streaming in Python APIresponses?

**Answer:** It sends partial model output as chunksinstead of waiting for the full answer.

### 78. What is Pydantic?

**Answer:** Pydantic validates and parses data using Python type hints.

### 79. Why use Pydantic in APIs?

**Answer:** It validates request and responseschemas, reducing bad inputs and runtime errors.

### 80. What is unit testing in Python?

**Answer:** Testing small functions independently tocheck correctness.

### 81. What is pytest?

**Answer:** pytest is a popular Python testing framework.

### 82. What is mocking?

**Answer:** Mocking replaces real dependencies with fake ones during tests.

### 83. Why mock LLM calls in tests?

**Answer:** It avoids cost, rate limits, randomness, andexternal dependency failures.

### 84. What is load testing?

**Answer:** Load testing checks how an app performs under many users or requests.

### 85. What is autoscaling?

**Answer:** Autoscaling automatically adjusts compute resources based on demand.

### 86. How do you improve Python API performance?

**Answer:** Use async calls, caching, connection pooling, smaller payloads, profiling, and scalable hosting.

### 87. What is connection pooling?

**Answer:** It reuses network/database connectionsinstead of creating new ones each time.

### 88. What is serialization?

**Answer:** Serialization converts data structures to formats like JSON for storage or transfer.

### 89. What is idempotency?

**Answer:** An operation is idempotent if repeating it produces the same final result.

### 90. Why is idempotency useful in cloud apps?

**Answer:** Retries may happen, and idempotencyprevents duplicate processing.

### 91. What is environment variable?

**Answer:** It is configuration stored outside code, often used for endpoints and settings.

### 92. How do you manage config across dev/test/prod?

**Answer:** Use separate environment variables, Key Vault, config files, and deployment settings.

### 93. What is blue-green deployment?

**Answer:** It uses two environments so traffic canswitch safely from old to new version.

### 94. What is canary deployment?

**Answer:** It releases a new version to a small usergroup before full rollout.

### 95. How would you build a Python RAG app on Azure?

**Answer:** Ingest documents to Blob, create embeddings, index in Azure AI Search, build FastAPI, call LLM, add monitoring and security.

### 96. What is an important interview point for Python on Azure?

**Answer:** Explain the concept simply, give a practicalexample, and mention trade-offs or limitations.

### 97. What is an important interview point for Python on Azure?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs orlimitations.

### 98. What is an important interview point for Python on Azure?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

### 99. What is an important interview point for Python on Azure?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs orlimitations.

### 100. What is an important interview point for Python on Azure?

**Answer:** Explain the concept simply, give a practical example, and mention trade-offs or limitations.

