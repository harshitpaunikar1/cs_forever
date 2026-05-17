# RAG

Retrieval-Augmented Generation interview question bank covering retrieval, embeddings, chunking, ranking, evaluation, and production readiness.

## Questions

### 1. What is Retrieval-Augmented Generation in RAG?

**Answer:** Retrieval-Augmented Generation is a pattern that retrieves relevant external knowledge and gives it to an LLM before generation.

### 2. Why does Retrieval-Augmented Generation matter in RAG interviews?

**Answer:** In RAG, Retrieval-Augmented Generation directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 3. How would you explain Retrieval-Augmented Generation in a project discussion?

**Answer:** In a project, explain that Retrieval-Augmented Generation connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 4. What is a common mistake with Retrieval-Augmented Generation?

**Answer:** A common mistake with Retrieval-Augmented Generation is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 5. What is knowledge base in RAG?

**Answer:** knowledge base is the indexed source of documents, FAQs, tickets, code, or records used for retrieval.

### 6. Why does knowledge base matter in RAG interviews?

**Answer:** In RAG, knowledge base directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 7. How would you explain knowledge base in a project discussion?

**Answer:** In a project, explain that knowledge base connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 8. What is a common mistake with knowledge base?

**Answer:** A common mistake with knowledge base is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 9. What is document ingestion in RAG?

**Answer:** document ingestion is the pipeline that loads, cleans, splits, enriches, and indexes source content.

### 10. Why does document ingestion matter in RAG interviews?

**Answer:** In RAG, document ingestion directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 11. How would you explain document ingestion in a project discussion?

**Answer:** In a project, explain that document ingestion connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 12. What is a common mistake with document ingestion?

**Answer:** A common mistake with document ingestion is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 13. What is chunking in RAG?

**Answer:** chunking is splitting documents into smaller meaningful passages that fit retrieval and model context.

### 14. Why does chunking matter in RAG interviews?

**Answer:** In RAG, chunking directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 15. How would you explain chunking in a project discussion?

**Answer:** In a project, explain that chunking connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 16. What is a common mistake with chunking?

**Answer:** A common mistake with chunking is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 17. What is chunk overlap in RAG?

**Answer:** chunk overlap is repeating a small part of neighboring chunks to preserve context across boundaries.

### 18. Why does chunk overlap matter in RAG interviews?

**Answer:** In RAG, chunk overlap directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 19. How would you explain chunk overlap in a project discussion?

**Answer:** In a project, explain that chunk overlap connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 20. What is a common mistake with chunk overlap?

**Answer:** A common mistake with chunk overlap is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 21. What is embedding model in RAG?

**Answer:** embedding model is a model that converts text into vectors so semantic similarity can be searched.

### 22. Why does embedding model matter in RAG interviews?

**Answer:** In RAG, embedding model directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 23. How would you explain embedding model in a project discussion?

**Answer:** In a project, explain that embedding model connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 24. What is a common mistake with embedding model?

**Answer:** A common mistake with embedding model is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 25. What is vector database in RAG?

**Answer:** vector database is a store optimized for embedding similarity search and metadata filtering.

### 26. Why does vector database matter in RAG interviews?

**Answer:** In RAG, vector database directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 27. How would you explain vector database in a project discussion?

**Answer:** In a project, explain that vector database connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 28. What is a common mistake with vector database?

**Answer:** A common mistake with vector database is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 29. What is semantic search in RAG?

**Answer:** semantic search is retrieval by meaning rather than exact keyword matching.

### 30. Why does semantic search matter in RAG interviews?

**Answer:** In RAG, semantic search directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 31. How would you explain semantic search in a project discussion?

**Answer:** In a project, explain that semantic search connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 32. What is a common mistake with semantic search?

**Answer:** A common mistake with semantic search is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 33. What is hybrid search in RAG?

**Answer:** hybrid search is combining keyword search and vector search to improve recall and precision.

### 34. Why does hybrid search matter in RAG interviews?

**Answer:** In RAG, hybrid search directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 35. How would you explain hybrid search in a project discussion?

**Answer:** In a project, explain that hybrid search connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 36. What is a common mistake with hybrid search?

**Answer:** A common mistake with hybrid search is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 37. What is metadata filtering in RAG?

**Answer:** metadata filtering is restricting retrieval by fields such as product, date, region, role, or document type.

### 38. Why does metadata filtering matter in RAG interviews?

**Answer:** In RAG, metadata filtering directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 39. How would you explain metadata filtering in a project discussion?

**Answer:** In a project, explain that metadata filtering connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 40. What is a common mistake with metadata filtering?

**Answer:** A common mistake with metadata filtering is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 41. What is top-k retrieval in RAG?

**Answer:** top-k retrieval is returning the k most similar chunks from the index for a query.

### 42. Why does top-k retrieval matter in RAG interviews?

**Answer:** In RAG, top-k retrieval directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 43. How would you explain top-k retrieval in a project discussion?

**Answer:** In a project, explain that top-k retrieval connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 44. What is a common mistake with top-k retrieval?

**Answer:** A common mistake with top-k retrieval is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 45. What is reranking in RAG?

**Answer:** reranking is using a stronger ranking model to reorder retrieved chunks by relevance.

### 46. Why does reranking matter in RAG interviews?

**Answer:** In RAG, reranking directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 47. How would you explain reranking in a project discussion?

**Answer:** In a project, explain that reranking connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 48. What is a common mistake with reranking?

**Answer:** A common mistake with reranking is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 49. What is query rewriting in RAG?

**Answer:** query rewriting is rewriting a user query into a clearer retrieval query before searching.

### 50. Why does query rewriting matter in RAG interviews?

**Answer:** In RAG, query rewriting directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 51. How would you explain query rewriting in a project discussion?

**Answer:** In a project, explain that query rewriting connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 52. What is a common mistake with query rewriting?

**Answer:** A common mistake with query rewriting is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 53. What is multi-query retrieval in RAG?

**Answer:** multi-query retrieval is generating multiple query variants to cover different phrasings of the same need.

### 54. Why does multi-query retrieval matter in RAG interviews?

**Answer:** In RAG, multi-query retrieval directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 55. How would you explain multi-query retrieval in a project discussion?

**Answer:** In a project, explain that multi-query retrieval connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 56. What is a common mistake with multi-query retrieval?

**Answer:** A common mistake with multi-query retrieval is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 57. What is context window in RAG?

**Answer:** context window is the token budget available for the prompt, retrieved context, instructions, and answer.

### 58. Why does context window matter in RAG interviews?

**Answer:** In RAG, context window directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 59. How would you explain context window in a project discussion?

**Answer:** In a project, explain that context window connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 60. What is a common mistake with context window?

**Answer:** A common mistake with context window is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 61. What is grounded generation in RAG?

**Answer:** grounded generation is answering only from retrieved evidence and avoiding unsupported claims.

### 62. Why does grounded generation matter in RAG interviews?

**Answer:** In RAG, grounded generation directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 63. How would you explain grounded generation in a project discussion?

**Answer:** In a project, explain that grounded generation connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 64. What is a common mistake with grounded generation?

**Answer:** A common mistake with grounded generation is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 65. What is citation generation in RAG?

**Answer:** citation generation is linking answer statements back to the source chunks used by the model.

### 66. Why does citation generation matter in RAG interviews?

**Answer:** In RAG, citation generation directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 67. How would you explain citation generation in a project discussion?

**Answer:** In a project, explain that citation generation connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 68. What is a common mistake with citation generation?

**Answer:** A common mistake with citation generation is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 69. What is hallucination control in RAG?

**Answer:** hallucination control is reducing unsupported answers through retrieval quality, prompts, and answer checks.

### 70. Why does hallucination control matter in RAG interviews?

**Answer:** In RAG, hallucination control directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 71. How would you explain hallucination control in a project discussion?

**Answer:** In a project, explain that hallucination control connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 72. What is a common mistake with hallucination control?

**Answer:** A common mistake with hallucination control is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 73. What is freshness in RAG?

**Answer:** freshness is keeping indexed content synchronized with the latest source documents.

### 74. Why does freshness matter in RAG interviews?

**Answer:** In RAG, freshness directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 75. How would you explain freshness in a project discussion?

**Answer:** In a project, explain that freshness connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 76. What is a common mistake with freshness?

**Answer:** A common mistake with freshness is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 77. What is access control in RAG?

**Answer:** access control is ensuring retrieval only returns documents the user is allowed to see.

### 78. Why does access control matter in RAG interviews?

**Answer:** In RAG, access control directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 79. How would you explain access control in a project discussion?

**Answer:** In a project, explain that access control connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 80. What is a common mistake with access control?

**Answer:** A common mistake with access control is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 81. What is evaluation dataset in RAG?

**Answer:** evaluation dataset is a set of test questions, expected answers, and relevant documents used to measure RAG quality.

### 82. Why does evaluation dataset matter in RAG interviews?

**Answer:** In RAG, evaluation dataset directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 83. How would you explain evaluation dataset in a project discussion?

**Answer:** In a project, explain that evaluation dataset connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 84. What is a common mistake with evaluation dataset?

**Answer:** A common mistake with evaluation dataset is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 85. What is retrieval metrics in RAG?

**Answer:** retrieval metrics is measurements such as recall at k, precision at k, MRR, and nDCG.

### 86. Why does retrieval metrics matter in RAG interviews?

**Answer:** In RAG, retrieval metrics directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 87. How would you explain retrieval metrics in a project discussion?

**Answer:** In a project, explain that retrieval metrics connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 88. What is a common mistake with retrieval metrics?

**Answer:** A common mistake with retrieval metrics is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 89. What is answer metrics in RAG?

**Answer:** answer metrics is measurements for groundedness, correctness, completeness, and faithfulness.

### 90. Why does answer metrics matter in RAG interviews?

**Answer:** In RAG, answer metrics directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 91. How would you explain answer metrics in a project discussion?

**Answer:** In a project, explain that answer metrics connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 92. What is a common mistake with answer metrics?

**Answer:** A common mistake with answer metrics is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 93. What is latency optimization in RAG?

**Answer:** latency optimization is reducing end-to-end time spent in rewriting, retrieval, reranking, and generation.

### 94. Why does latency optimization matter in RAG interviews?

**Answer:** In RAG, latency optimization directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 95. How would you explain latency optimization in a project discussion?

**Answer:** In a project, explain that latency optimization connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 96. What is a common mistake with latency optimization?

**Answer:** A common mistake with latency optimization is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

### 97. What is production monitoring in RAG?

**Answer:** production monitoring is tracking quality, failures, costs, latency, drift, and user feedback in a live RAG system.

### 98. Why does production monitoring matter in RAG interviews?

**Answer:** In RAG, production monitoring directly affects retrieval precision, grounding, citation quality, latency, and document access control. A good answer should show when you would use it, how you would measure it, and what can break if it is designed poorly.

### 99. How would you explain production monitoring in a project discussion?

**Answer:** In a project, explain that production monitoring connects user intent to the right evidence before generation. Describe the input it receives, the output it produces, the metric it improves, and the operational checks you would add before production.

### 100. What is a common mistake with production monitoring?

**Answer:** A common mistake with production monitoring is adding more chunks or a larger model without measuring retrieval quality, grounding, and source coverage. The better approach is to test it with realistic data, monitor failures, and document the trade-off clearly.

