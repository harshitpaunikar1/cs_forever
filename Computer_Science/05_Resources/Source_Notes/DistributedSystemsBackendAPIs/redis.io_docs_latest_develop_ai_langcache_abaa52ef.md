Title: Redis LangCache | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/ai/langcache/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:50+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# Redis LangCache

Store LLM responses for AI apps in a semantic cache.

Redis LangCache is a fully-managed semantic caching service that reduces large language model (LLM) costs and improves response times for AI applications.

[Get started](https://redis.io#get-started) with LangCache on [Redis Cloud](https://redis.io/docs/latest/operate/rc/langcache/) or join the [private preview](https://redis.io/langcache/).

##
LangCache overview
[
](https://redis.io#langcache-overview)

LangCache uses semantic caching to store and reuse previous LLM responses for repeated queries. Instead of calling the LLM for every request, LangCache checks if a similar response has already been generated and is stored in the cache. If a match is found, LangCache returns the cached response instantly, saving time and resources.

Imagine youâre using an LLM to build an agent to answer questions about your company's products. Your users may ask questions like the following:

- "What are the features of Product A?"
- "Can you list the main features of Product A?"
- "Tell me about Product Aâs features."

These prompts may have slight variations, but they essentially ask the same question. LangCache can help you avoid calling the LLM for each of these prompts by caching the response to the first prompt and returning it for any similar prompts.

Using LangCache as a semantic caching service has the following benefits:

**Lower LLM costs**: Reduce costly LLM calls by easily storing the most frequently-requested responses.**Faster AI app responses**: Get faster AI responses by retrieving previously-stored requests from memory.**Simpler deployments**: Access our managed service using a REST API with automated embedding generation, configurable controls, and no database management required.**Advanced cache management**: Manage data access, privacy, and eviction protocols. Monitor usage and cache hit rates.

LangCache works well for the following use cases:

**AI assistants and chatbots**: Optimize conversational AI applications by caching common responses and reducing latency for frequently asked questions.**RAG applications**: Enhance retrieval-augmented generation performance by caching responses to similar queries, reducing both cost and response time.**AI agents**: Improve multi-step reasoning chains and agent workflows by caching intermediate results and common reasoning patterns.**AI gateways**: Integrate LangCache into centralized AI gateway services to manage and control LLM costs across multiple applications..

###
LLM cost reduction with LangCache
[
](https://redis.io#llm-cost-reduction-with-langcache)

LangCache reduces your LLM costs by caching responses and avoiding repeated API calls. When a response is served from cache, you donât pay for output tokens. Input token costs are typically offset by embedding and storage costs.

For every cached response, you'll save the output token cost. To calculate your monthly savings with LangCache, you can use the following formula:

```
Est. monthly savings with LangCache =
(Monthly output token costs) Ã (Cache hit rate)
```

The more requests you serve from LangCache, the more you save, because youâre not paying to regenerate the output.

Hereâs an example:

- Monthly LLM spend: $200
- Percentage of output tokens in your spend: 60%
- Cost of output tokens: $200 Ã 60% = $120
- Cache hit rate: 50%
- Estimated savings: $120 Ã 50% = $60/month

You can also use the [LangCache savings calculator](https://redis.io/calculator/langcache/) to estimate your annual savings with LangCache.

##
LangCache architecture
[
](https://redis.io#langcache-architecture)

The following diagram displays how you can integrate LangCache into your GenAI app:

- A user sends a prompt to your AI app.
- Your app sends the prompt to LangCache through the
`POST /v1/caches/{cacheId}/entries/search`

endpoint. - LangCache calls an embedding model service to generate an embedding for the prompt.
- LangCache searches the cache to see if a similar response already exists by matching the embeddings of the new query with the stored embeddings.
- If a semantically similar entry is found (also known as a cache hit), LangCache gets the cached response and returns it to your app. Your app can then send the cached response back to the user.
- If no match is found (also known as a cache miss), your app receives an empty response from LangCache. Your app then queries your chosen LLM to generate a new response.
- Your app sends the prompt and the new response to LangCache through the
`POST /v1/caches/{cacheId}/entries`

endpoint. - LangCache stores the embedding with the new response in the cache for future use.

See the [LangCache API and SDK examples](https://redis.io/docs/latest/develop/ai/langcache/api-examples/) for more information on how to use the LangCache API.

##
Get started
[
](https://redis.io#get-started)

LangCache is currently in preview:

- Public preview on
[Redis Cloud](https://redis.io/docs/latest/operate/rc/langcache/) - Fully-managed
[private preview](https://redis.io/langcache/)

To set up LangCache on Redis Cloud:

[Create a database](https://redis.io/docs/latest/operate/rc/databases/create-database/)on Redis Cloud.[Create a LangCache service](https://redis.io/docs/latest/operate/rc/langcache/create-service/)for your database on Redis Cloud.[Use the LangCache API](https://redis.io/docs/latest/operate/rc/langcache/use-langcache/)from your client app.

After you set up LangCache, you can [view and edit the cache](https://redis.io/docs/latest/operate/rc/langcache/view-edit-cache/) and [monitor the cache's performance](https://redis.io/docs/latest/operate/rc/langcache/monitor-cache/).

See also our [Redis LangCache setup](https://www.youtube.com/watch?v=UOGhMZlZLko)
tutorial video for advice on how to get started.
