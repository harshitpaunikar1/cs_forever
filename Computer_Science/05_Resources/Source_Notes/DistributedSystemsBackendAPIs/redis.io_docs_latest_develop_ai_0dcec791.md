Title: Redis for AI and search | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/ai/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:49+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# Redis for AI and search

An overview of Redis for AI and search documentation

Redis stores and indexes vector embeddings that semantically represent unstructured data including text passages, images, videos, or audio. Store vectors and the associated metadata within [hashes](https://redis.io/docs/latest/develop/data-types/hashes/) or [JSON](https://redis.io/docs/latest/develop/data-types/json/) documents for [indexing](https://redis.io/docs/latest/develop/ai/search-and-query/indexing/) and [querying](https://redis.io/docs/latest/develop/ai/search-and-query/query/).

[
Redis vector Python client library documentation
](https://redis.io/docs/latest/develop/ai/redisvl/)

[
Use Redis Search to search data
](https://redis.io/docs/latest/develop/ai/search-and-query/)

[
Use LangCache to store LLM responses
](https://redis.io/docs/latest/develop/ai/langcache/)

##
Featureform
[
](https://redis.io#featureform)

Use [Featureform](https://redis.io/docs/latest/develop/ai/featureform/) to define, manage, and serve machine learning features on top of your existing data systems. The Featureform docs cover the Python SDK workflow from provider registration through feature serving.

####
Overview
[
](https://redis.io#overview)

This page is organized into a few sections depending on what you're trying to do:

**How to's**- The comprehensive reference section for every feature, API, and setting. It's your source for detailed, technical information to support any level of development.**Concepts**- Explanations of foundational ideas and core principles to help you understand the reason behind the product's features and design.**Quickstarts**- Short, focused guides to get you started with key features or workflows in minutes.**Tutorials**- In-depth walkthroughs that dive deeper into specific use cases or processes. These step-by-step guides help you master essential tasks and workflows.**Integrations**- Guides and resources to help you connect and use the product with popular tools, frameworks, or platforms.**Video tutorials**- Watch our AI video collection featuring practical tutorials and demonstrations.**Benchmarks**- Performance comparisons and metrics to demonstrate how the product performs under various scenarios. This helps you understand its efficiency and capabilities.**Best practices**- Recommendations and guidelines for maximizing effectiveness and avoiding common pitfalls. This section equips you to use the product effectively and efficiently.

##
How to's
[
](https://redis.io#how-tos)

: Redis maintains a secondary index over your data with a defined schema (including vector fields and metadata). Redis supports**Create a vector index**and`FLAT`

vector index types.`HNSW`

: Redis stores vectors and metadata in hashes or JSON objects.**Store and update vectors**: Redis supports several advanced querying strategies with vector fields including k-nearest neighbor (**Search with vectors**[KNN](https://redis.io/docs/latest/develop/ai/search-and-query/vectors/#knn-vector-search)),[vector range queries](https://redis.io/docs/latest/develop/ai/search-and-query/vectors/#vector-range-queries), and[metadata filters](https://redis.io/docs/latest/develop/ai/search-and-query/vectors/#filters).. Select the best filter mode to optimize query execution.**Configure vector queries at runtime**

####
Learn how to index and query vector embeddings
[
](https://redis.io#learn-how-to-index-and-query-vector-embeddings)

##
Concepts
[
](https://redis.io#concepts)

Learn to perform vector search and use gateways and semantic caching in your AI/ML projects.

[
Vector search guide
](https://redis.io/docs/latest/develop/ai/search-and-query/query/vector-search/)

[
Store memory for LLMs
](https://redis.io/blog/level-up-rag-apps-with-redis-vector-library/)

[
Semantic caching for faster, smarter LLM apps
](https://redis.io/blog/what-is-semantic-caching)

[
Semantic routing chooses the best tool
](https://redis.io/blog/level-up-rag-apps-with-redis-vector-library/)

[
Deploy an enhanced gateway with Redis
](https://redis.io/blog/ai-gateways-what-are-they-how-can-you-deploy-an-enhanced-gateway-with-redis/)

##
Quickstarts
[
](https://redis.io#quickstarts)

Quickstarts or recipes are useful when you are trying to build specific functionality. For example, you might want to do RAG with LangChain or set up LLM memory for your AI agent.

Get started with these foundational guides:

####
RAG
[
](https://redis.io#rag)

Retrieval Augmented Generation (aka RAG) is a technique to enhance the ability of an LLM to respond to user queries. The retrieval part of RAG is supported by a vector database, which can return semantically relevant results to a user's query, serving as contextual information to augment the generative capabilities of an LLM.

Explore our [AI notebooks collection](https://redis.io/docs/latest/develop/ai/notebook-collection/) for comprehensive RAG examples including:

- RAG implementations with RedisVL, LangChain, and LlamaIndex
- Advanced RAG techniques and optimizations
- RAG evaluation with the RAGAS framework
- Integration with cloud platforms like Azure and Vertex AI

Additional resources:

####
Agents
[
](https://redis.io#agents)

AI agents can act autonomously to plan and execute tasks for the user.

##
Tutorials
[
](https://redis.io#tutorials)

Need a deeper-dive through different use cases and topics?

####
RAG
[
](https://redis.io#rag-1)

[Agentic RAG](https://github.com/redis-developer/agentic-rag)- A tutorial focused on agentic RAG with LlamaIndex and Amazon Bedrock[RAG on Vertex AI](https://github.com/redis-developer/gcp-redis-llm-stack/tree/main)- A RAG tutorial featuring Redis with Vertex AI[RAG workbench](https://github.com/redis-developer/redis-rag-workbench)- A development playground for exploring RAG techniques with Redis[ArXiv Chat](https://github.com/redis-developer/ArxivChatGuru)- Streamlit demo of RAG over ArXiv documents with Redis & OpenAI

####
Recommendations and search
[
](https://redis.io#recommendations-and-search)

[Recommendation systems w/ NVIDIA Merlin & Redis](https://github.com/redis-developer/redis-nvidia-recsys)- Three examples, each escalating in complexity, showcasing the process of building a realtime recsys with NVIDIA and Redis[Redis product search](https://github.com/redis-developer/redis-product-search)- Build a real-time product search engine using features like full-text search, vector similarity, and real-time data updates[ArXiv Search](https://github.com/redis-developer/redis-arxiv-search)- Full stack implementation of Redis with React FE

##
Ecosystem integrations
[
](https://redis.io#ecosystem-integrations)

Explore our comprehensive [ecosystem integrations page](https://redis.io/docs/latest/develop/ai/ecosystem-integrations/) to discover how Redis works with popular AI frameworks, platforms, and tools including:

- LangGraph, LangChain, and LlamaIndex for building advanced AI applications
- Amazon Bedrock and NVIDIA NIM for enhanced AI infrastructure
- Microsoft Semantic Kernel and Kernel Memory for LLM applications
- And many more integrations to power your AI solutions

##
Video tutorials
[
](https://redis.io#video-tutorials)

Watch our [AI video collection](https://redis.io/docs/latest/develop/ai/ai-videos/) featuring practical tutorials and demonstrations on:

- Building RAG applications and implementing vector search
- Working with LangGraph for AI agents with memory
- Semantic caching and search techniques
- Redis integrations with popular AI frameworks
- Real-world AI application examples and best practices

##
Benchmarks
[
](https://redis.io#benchmarks)

See how we stack up against the competition.

##
Best practices
[
](https://redis.io#best-practices)

See how leaders in the industry are building their RAG apps.
