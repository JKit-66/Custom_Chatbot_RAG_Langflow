# Personalized RAG Chatbot with Langflow, Gemini & Astra DB
An end-to-end Retrieval-Augmented Generation (RAG) project that builds a personalized chatbot capable of answering questions from a specific knowledge base. This project leverages the visual orchestration of Langflow, the powerful generative capabilities of Google's Gemini API, and the scalable vector storage of Astra DB.

## About The Project
General-purpose Large Language Models (LLMs) are incredibly powerful but lack knowledge of private, specific, or recent documents. This project solves that problem by implementing a RAG pipeline.

The system ingests a user-provided document (e.g., a PDF document), processes its content into a searchable vector format, and stores it in Astra DB. When a user asks a question, the system retrieves the most relevant information from the document and provides it to the Gemini API as context, enabling it to generate an accurate, fact-based answer. 

## Key Features
- **Document Ingestion**: Supports various document formats to create a custom knowledge base.
- **Conversational Memory**: Remembers previous user questions and AI answers to understand context in follow-up queries.
- **Dynamic Context Retrieval**: Uses vector similarity search in Astra DB to find the most relevant document chunks for any given query.
- **Context-Aware Generation**: Injects retrieved context into prompts for the Gemini API to ensure answers are grounded in the source material and minimize hallucinations.

📄 License
This project is licensed under the MIT License - see the ```LICENSE``` file for details.