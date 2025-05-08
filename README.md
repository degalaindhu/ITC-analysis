
# 📄 ITC Financial Analysis with AI

This document explains step-by-step what I implemented in my project, which focuses on extracting and analyzing financial data from ITC Limited’s annual reports using web scraping and large language models (LLMs).

---

## 🔧 1. **Installed Required Libraries**

I began by installing all necessary Python packages:

* `langchain`, `langchain-openai`, `langchain-community`, `langchain-huggingface` for document processing and LLM orchestration.
* `tavily-python` for scraping and extracting content from web-based PDF documents.
* `langchain_chroma` for storing and searching embeddings using a vector database.

---

## 🔑 2. **Set Up API Clients**

I initialized two main APIs:

* **Tavily Client** for extracting structured text from the ITC annual report URLs.
* **OpenAI** for generating embeddings and using a language model for question answering.

I provided my Tavily API key directly and read the OpenAI key from a text file.

---

## 📄 3. **Extracted Text from Annual Reports**

I passed the 2023 and 2024 ITC annual report URLs to Tavily’s extract function. This extracted the **raw content** from both PDF documents, which included financial data, performance metrics, and other business details.

---

## 🗂️ 4. **Created Document Objects**

I converted the extracted text from each PDF into LangChain `Document` objects. This step allowed me to store metadata (like the source URL) along with the actual content for easier processing.

---

## ✂️ 5. **Split Large Text into Chunks**

To manage the large amount of text, I used LangChain’s `RecursiveCharacterTextSplitter` to break the content into chunks of 300 characters, with 50-character overlaps. This was important for handling token limits and preserving context for analysis.

---

## 📊 6. **Generated Embeddings**

Using OpenAI’s `OpenAIEmbeddings` module, I converted each text chunk into an embedding — a numerical vector representing the meaning of the text. These embeddings are essential for semantic search.

---

## 🧠 7. **Stored Embeddings in Chroma Vector Database**

I stored all the generated embeddings in a Chroma vector database. This allowed me to later search for relevant chunks of text based on the semantic similarity to user questions.

I verified that the documents were added successfully by checking the number of stored document IDs.

---

## ❓ 8. **Performed Semantic Search**

I wrote a question:
**“What is the revenue of ITC in 2024?”**

Then, using Chroma’s similarity search, I retrieved the top 3 most relevant text chunks from the database. I combined them into a single context string for further analysis.

---

## 💬 9. **Created a Prompt for the Language Model**

I defined a prompt using LangChain’s `ChatPromptTemplate`. The prompt instructed the model to:

* Answer the question **based only on the retrieved context**
* Avoid adding unrelated justifications
* Provide a **detailed and concise** response

---

## 🤖 10. **Answered the Question Using ChatGPT**

I passed the context and question to the `ChatOpenAI` model and received a detailed response about ITC’s 2024 revenue. This confirmed the end-to-end pipeline — from extraction to answering — was working as expected.

---


## 📘 Conclusion

In this project, I built a complete AI-based pipeline to extract and analyze financial data from annual reports. By combining web scraping, document chunking, vector storage, and LLM-based reasoning, I created a system capable of answering natural language questions like “What was ITC’s revenue in 2024?” directly from unstructured documents.

---

Let me know if you'd like this turned into a PDF, DOCX, or formatted for slides.
