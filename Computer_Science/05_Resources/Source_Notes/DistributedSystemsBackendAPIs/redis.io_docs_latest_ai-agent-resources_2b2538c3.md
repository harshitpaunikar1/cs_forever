Title: AI Agent Resources | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/ai-agent-resources/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:45+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# AI Agent Resources

Learn how to develop with Redis as an AI agent

##
`llms.txt`

index of documentation
[
](https://redis.io#llmstxt-index-of-documentation)

Redis provides a comprehensive index of all documentation in Markdown format at [llms.txt](https://redis.io/llms.txt). This index is specifically designed for AI agents to discover available documentation.

##
Markdown documentation format
[
](https://redis.io#markdown-documentation-format)

All documentation pages are available in Markdown format via the same URL as
the main doc page but with `index.html.md`

added. For example, the Markdown version of
this page is available at
[ai-agent-resources/index.html.md](https://redis.io/docs/latest/ai-agent-resources/index.html.md).

##
JSON documentation feeds
[
](https://redis.io#json-documentation-feeds)

Redis documentation is available in structured JSON format optimized for RAG (Retrieval-Augmented Generation) systems.

###
NDJSON feed (all pages)
[
](https://redis.io#ndjson-feed-all-pages)

A single file containing all documentation pages in [NDJSON](https://github.com/ndjson/ndjson-spec) format (one JSON object per line):

| Format | URL | Size |
|---|---|---|
| NDJSON |
|

[docs.ndjson.gz](https://redis.io/docs/latest/docs.ndjson.gz)Both files contain ~4,100 documents.

###
Per-page JSON
[
](https://redis.io#per-page-json)

Each documentation page has a corresponding JSON file at the same URL with `/index.json`

appended. For example:

- Page:
`https://redis.io/docs/latest/commands/set/`

- JSON:
`https://redis.io/docs/latest/commands/set/index.json`

###
JSON schema
[
](https://redis.io#json-schema)

Each document contains:

| Field | Type | Description |
|---|---|---|
`id` |
string | URL slug identifier |
`title` |
string | Page title |
`url` |
string | Canonical URL |
`summary` |
string | Short description |
`page_type` |
string | `"content"` (has prose) or `"index"` (navigation only) |
`content_hash` |
string | SHA256 hash for cache invalidation (content pages only) |
`sections` |
array | Content split by headings with semantic roles |
`examples` |
array | Code blocks extracted from content |
`children` |
array | Child pages (index pages only) |

Each **section** contains:

`id`

: Slugified heading`title`

: Original heading text`role`

: Semantic role (`overview`

,`syntax`

,`example`

,`parameters`

,`returns`

, etc.)`text`

: Section content (code blocks replaced with`[code example]`

placeholder)

Each **example** contains:

`id`

: Unique identifier (`{section_id}-ex{index}`

)`language`

: Language from code fence (`python`

,`go`

,`plaintext`

, etc.)`code`

: The code content`section_id`

: Which section this example came from

###
Verifying content_hash
[
](https://redis.io#verifying-content_hash)

The `content_hash`

can be verified by computing:

```
import hashlib
def verify_hash(page):
parts = [page.get('summary', '')]
for section in page.get('sections', []):
parts.append(section['text'])
for example in page.get('examples', []):
parts.append(example['code'])
content = '\n'.join(parts)
return hashlib.sha256(content.encode('utf-8')).hexdigest() == page.get('content_hash')
```

##
API references
[
](https://redis.io#api-references)

API references are available for the following client libraries:

##
Data type comparisons
[
](https://redis.io#data-type-comparisons)

See [Compare data types](https://redis.io/docs/latest/develop/data-types/compare-data-types/) for advice
on which of the general-purpose data types is best for common tasks.

##
Redis patterns for coding agents
[
](https://redis.io#redis-patterns-for-coding-agents)

Salvatore Sanfilippo (also known as *antirez*, the creator of Redis) has provided the Redis community with a resource containing very useful Redis-oriented design patterns. See [this page](https://redis.antirez.com/) for more information.

##
Error handling
[
](https://redis.io#error-handling)

See [Error handling](https://redis.io/docs/latest/develop/clients/error-handling/) for a guide to handling errors in client libraries.
