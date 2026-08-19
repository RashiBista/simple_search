## RAG

RAG (Retrieval-Augmented Generation) is an artificial intelligence technique that improves large language model (LLM) responses by fetching relevant facts from an external knowledge base before generating an answer. It prevents guessing (hallucinations) and lets models use private data without expensive retraining
---
How RAG Works: 
- Documents are split into small pieces (chunks), converted into numerical vector embeddings, and saved in a vector database
- Retrieval: When you ask a question, the system converts your query into a vector and searches the database for text chunks with matching meaning.
- Augmentation: The system combines your original question with the retrieved text snippets into a single prompt.
- Generation: The LLM reads the custom prompt and writes an accurate, context-aware answer based on those specific retrieved facts.Why RAG is Used
