# Large Language Models (LLMs)

Interview question bank from `LLM_Azure_AI_Interview_700_QA.docx`.

## Questions

### 1. What is a Large Language Model?

**Answer:** An LLM is an AI model trained on huge text data to understand and generate human-like language.

### 2. What is a token?

**Answer:** A token is a small text unit, such as a word, part of a word, number, or symbol, that a model processes.

### 3. Why do LLMs use tokens instead of full words?

**Answer:** Tokens handle many languages, rare words, code, and subwords more efficiently than fixed word lists.

### 4. What is next-token prediction?

**Answer:** It is the training task where the model learns to predict the next token based onprevious tokens.

### 5. What is a transformer?

**Answer:** A transformer is a neural network architecture that uses attention to understand relationships between tokens.

### 6. What is self-attention?

**Answer:** Self-attention lets each token look at other tokens in the input and decide which onesmatter most.

### 7. What is multi-head attention?

**Answer:** It runs multiple attention mechanisms in parallel so the model can learn differentrelationships at once.

### 8. What are embeddings?

**Answer:** Embeddings are numerical vector representations of text that capture meaning and similarity.

### 9. What is positional encoding?

**Answer:** It tells the transformer the order of tokens, because attention alone does not knowsequence position.

### 10. What is context window?

**Answer:** It is the maximum amount of tokens the model can read and use at one time.

### 11. What is prompt engineering?

**Answer:** Prompt engineering is writing clear instructions and examples to guide modeloutput.

### 12. What is zero-shot prompting?

**Answer:** The model answers a task without examples, using only the instruction.

### 13. What is few-shot prompting?

**Answer:** The prompt includes a few examples so the model can follow the same pattern.

### 14. What is chain-of-thought prompting?

**Answer:** It encourages step-by-step reasoning, but in production we often ask for concise reasoning or final rationale.

### 15. What is temperature?

**Answer:** Temperature controls randomness; low values give consistent answers, highvalues give more creative answers.

### 16. What is top-p sampling?

**Answer:** Top-p limits token choices to the most likely group whose probabilities add up to p.

### 17. What is hallucination?

**Answer:** Hallucination is when the model gives an answer that sounds correct but is factually wrong or unsupported.

### 18. How can hallucinations be reduced?

**Answer:** Use grounding data, RAG, citations, validation, lower temperature, and cleartask boundaries.

### 19. What is fine-tuning?

**Answer:** Fine-tuning trains an existing model further on task-specific examples to improve behavior for that task.

### 20. What is instruction tuning?

**Answer:** Instruction tuning trains a model to follow natural-language instructions better.

### 21. What is RLHF?

**Answer:** RLHF uses human feedback to make model responses more helpful, safe, and aligned.

### 22. What is RAG?

**Answer:** Retrieval-Augmented Generation fetches relevant documents and gives them to the LLM before answering.

### 23. Why use RAG instead of fine-tuning?

**Answer:** RAG is better for changing knowledge because you update documents instead of retraining the model.

### 24. What is semantic search?

**Answer:** Semantic search finds text by meaning using embeddings, not only keyword matching.

### 25. What is vector database?

**Answer:** A vector database stores embeddings andsupports similarity search.

### 26. What is cosine similarity?

**Answer:** It measures how close two vectors point in the same direction, often used for embedding similarity.

### 27. What is chunking?

**Answer:** Chunking splits documents into smaller pieces so they fit into retrieval and modelcontext.

### 28. What makes good chunks?

**Answer:** Good chunks are meaningful, not too long, include enough context, and avoid cutting important ideas.

### 29. What is reranking?

**Answer:** Reranking reorders retrieved documents using a stronger model to put the most relevant results first.

### 30. What is grounding?

**Answer:** Grounding means making the model answer based on provided trusted datainstead of memory alone.

### 31. What is model evaluation?

**Answer:** It is measuring model quality using test cases, human review, automated metrics, and production feedback.

### 32. What metrics are used for LLM apps?

**Answer:** Common metrics include accuracy, faithfulness, relevance, latency, cost, safety, and user satisfaction.

### 33. What is BLEU?

**Answer:** BLEU measures overlap between generated text and reference text, mainly for translation-style tasks.

### 34. What is ROUGE?

**Answer:** ROUGE measures text overlap, often usedfor summarization evaluation.

### 35. What is perplexity?

**Answer:** Perplexity measures how surprised a language model is by text; lower usually means better language modeling.

### 36. What is latency in LLM apps?

**Answer:** Latency is the time between sending arequest and receiving a useful response.

### 37. What affects LLM cost?

**Answer:** Cost depends on input tokens, output tokens, model choice, calls to tools, and traffic volume.

### 38. How do you reduce LLM cost?

**Answer:** Use smaller models, shorter prompts, caching, batching, better retrieval, and limit unnecessary output.

### 39. What is prompt injection?

**Answer:** Prompt injection is an attack where user ordocument text tries to override system instructions.

### 40. How do you defend against prompt injection?

**Answer:** Separate trusted instructions from untrusted data, validate tool calls, restrictpermissions, and monitor outputs.

### 41. What is model alignment?

**Answer:** Alignment means making model behavior match human goals, policies, and safety expectations.

### 42. What is bias in LLMs?

**Answer:** Bias is unfair or skewed behavior learned from training data or design choices.

### 43. What is toxicity detection?

**Answer:** It checks whether model input or output contains harmful, abusive, or unsafe content.

### 44. What is moderation?

**Answer:** Moderation filters or flags content thatviolates safety rules.

### 45. What is system prompt?

**Answer:** A system prompt is a high-priority instruction that defines role, rules, and behavior.

### 46. What is user prompt?

**Answer:** A user prompt is the request or instruction given by the end user.

### 47. What is an assistant message?

**Answer:** It is the model's generated response in a conversation.

### 48. What is function calling/tool calling?

**Answer:** It lets the model request external functions or APIs in a structured way.

### 49. Why is tool calling useful?

**Answer:** It allows the LLM to get live data, performactions, calculate, search, or interact with systems.

### 50. What is JSON mode/structured output?

**Answer:** It forces or guides the model to return datain a defined JSON-like structure.

### 51. What is schema validation?

**Answer:** It checks whether model output follows expected fields, types, and rules.

### 52. What is a guardrail?

**Answer:** A guardrail is a rule, check, or control thatkeeps an LLM app safe and reliable.

### 53. What is context stuffing?

**Answer:** It means putting too much irrelevant information into the prompt, which increases cost and may reduce quality.

### 54. What is context compression?

**Answer:** It summarizes or filters context so only useful information is sent to the model.

### 55. What is long-context modeling?

**Answer:** It means a model can process very largeinputs, such as long documents or codebases.

### 56. What is attention complexity?

**Answer:** Standard attention can become expensive as sequence length grows because eachtoken compares with many tokens.

### 57. What is quantization?

**Answer:** Quantization reduces model number precision to make inference faster and cheaper, often with small quality tradeoffs.

### 58. What is distillation?

**Answer:** Distillation trains a smaller model to imitate a larger model.

### 59. What is LoRA?

**Answer:** LoRA is a parameter-efficient fine-tuning method that trains small adapter weights instead of the whole model.

### 60. What is PEFT?

**Answer:** Parameter-Efficient Fine-Tuning updatesonly a small part of a model to reduce training cost.

### 61. What is inference?

**Answer:** Inference is running a trained model togenerate output for a new input.

### 62. What is training?

**Answer:** Training is adjusting model weights using data so the model learns patterns.

### 63. What is pretraining?

**Answer:** Pretraining is the initial large-scale training on broad data before task-specific tuning.

### 64. What is supervised fine-tuning?

**Answer:** It trains the model on input-output examples created or approved by humans.

### 65. What is model deployment?

**Answer:** Deployment makes the model availablethrough an API or service for real users.

### 66. What is rate limiting?

**Answer:** Rate limiting controls how many requests can be sent in a time period.

### 67. What is batching?

**Answer:** Batching processes multiple requests together to improve throughput.

### 68. What is streaming response?

**Answer:** Streaming sends tokens as they aregenerated so users see output faster.

### 69. What is caching in LLM apps?

**Answer:** Caching stores previous responses or retrieval results to avoid repeated expensive work.

### 70. What is conversation memory?

**Answer:** Memory stores useful previous conversation information so future responses have continuity.

### 71. What is summarization memory?

**Answer:** It compresses previous conversation into a summary to fit within context limits.

### 72. What is retrieval memory?

**Answer:** It stores past information in searchable form and retrieves relevant parts whenneeded.

### 73. What is agentic reasoning?

**Answer:** It is when the model plans steps, uses tools, observes results, and continues until the task is done.

### 74. What is autonomous agent risk?

**Answer:** An agent may take wrong actions, call tools incorrectly, leak data, or loop withoutcontrols.

### 75. How do you evaluate a RAG system?

**Answer:** Check retrieval relevance, answer faithfulness, source citation quality, latency, and user task success.

### 76. What is faithfulness?

**Answer:** Faithfulness means the answer is supported by the provided context and does not invent details.

### 77. What is answer relevance?

**Answer:** Answer relevance measures whether the response directly answers the user's question.

### 78. What is retrieval recall?

**Answer:** Retrieval recall checks whether the system found the documents needed to answercorrectly.

### 79. What is embedding drift?

**Answer:** Embedding drift happens when models or data change and similarity behavior changes over time.

### 80. What is data leakage?

**Answer:** Data leakage is exposing private or training/test information where it should notbe available.

### 81. What is PII?

**Answer:** PII is personally identifiable information, such as phone numbers, emails, IDs, or addresses.

### 82. How should PII be handled in LLM apps?

**Answer:** Mask, minimize, encrypt, restrict access,log carefully, and follow privacy policies.

### 83. What is a model card?

**Answer:** A model card documents a model's purpose, limitations, evaluation, and responsible-use guidance.

### 84. What is red teaming?

**Answer:** Red teaming tests a model or app with adversarial prompts to find safety and reliability weaknesses.

### 85. What is fallback strategy?

**Answer:** It is a backup path when the model fails, such as asking clarification, using a smaller answer, or routing to humans.

### 86. What is human-in-the-loop?

**Answer:** A human reviews or approves modeloutputs or actions before final use.

### 87. What is deterministic output?

**Answer:** It means the same input usually gives the same output, often achieved with low temperature and fixed settings.

### 88. What is non-determinism in LLMs?

**Answer:** It means outputs can vary because generation involves probabilities andinfrastructure behavior.

### 89. What is maximum output token limit?

**Answer:** It controls the maximum number of tokens the model can generate in a response.

### 90. What is stop sequence?

**Answer:** A stop sequence tells the model where tostop generating.

### 91. What is model routing?

**Answer:** Model routing sends tasks to different models based on cost, complexity, latency, or quality needs.

### 92. What is a small language model?

**Answer:** An SLM is a smaller model optimized for lower cost, faster speed, or edge/private deployment.

### 93. When would you use a smaller model?

**Answer:** Use it for simple classification, extraction,summarization, or high-volume tasks where cost matters.

### 94. What is multimodal LLM?

**Answer:** It can process more than text, such asimages, audio, or video.

### 95. What is a vision-language model?

**Answer:** It understands both images and text and can answer questions about visual content.

### 96. What is speech-to-text in AI apps?

**Answer:** It converts spoken audio into text that an LLM or system can process.

### 97. What is text-to-speech in AI apps?

**Answer:** It converts generated text into spokenaudio.

### 98. How do you explain LLM limitations to a client?

**Answer:** I say LLMs are powerful language enginesbut need grounding, validation, and monitoring for business-critical use.

### 99. How would you design a chatbot using an LLM?

**Answer:** I would define scope, connect data with RAG, add guardrails, build APIs, test quality, monitor logs, and improvecontinuously.

### 100. What is prompt evaluation?

**Answer:** Prompt evaluation means testing different prompt versions to see which gives the most accurate, safe, and useful output.

