# **ArXivIntelliRAG: Your AI Agent for Relevant Research**

### **Project Overview**
**ArXivIntelliRAG** is a smart and personalized academic assistant that helps researchers find, understand, and summarize academic papers—exactly when they need them. By blending retrieval-augmented generation (RAG) with cutting-edge semantic search and summarization techniques, this AI-powered tool simplifies the research journey from discovery to comprehension.

---

### **Key Features**

1. **Academic Paper Retrieval**  
   - Fetches relevant papers in real-time from the **arXiv API** using keyword-based search.  
   - Stores and indexes abstracts using **FAISS** and **sentence-transformer embeddings** for fast semantic search.

2. **Semantic Ranking with SciBERT**  
   - Uses a pre-trained **SciBERT model** to rank retrieved papers based on textual similarity to the user’s query.  
   - Prioritizes documents with higher semantic relevance, even if they don’t share exact words.

3. **Summary Generation with LLM**  
   - Leverages **Ollama's LLaMA 3.2** model via **LangChain** to generate simplified summaries of top-ranked papers.  
   - Produces concise explanations tailored to the user’s query.

4. **User-Driven Query Input**  
   - Allows the user to input custom queries that are used to retrieve and rank papers from the local FAISS store.  
   - Highlights how the same dataset can be queried from different angles without redownloading data.

---

### **Skills Demonstrated**

- **Retrieval-Augmented Generation (RAG)**: Combines vector-based document retrieval with LLM-based summarization.  
- **Document Embedding**: Uses **sentence-transformers/all-MiniLM-L6-v2** to encode abstracts into vector space.  
- **Semantic Search**: Implements **FAISS** for scalable similarity-based retrieval.  
- **Relevance Ranking**: Applies **SciBERT** with softmax scoring to detect which documents are most contextually similar.  
- **LLM Summarization**: Uses LangChain and Ollama to generate human-readable summaries.  
- **LangChain Integration**: Seamlessly connects all modules into a unified processing pipeline.

---

### **Code Workflow**

#### **1. Data Preparation**
- Scrape academic paper abstracts from the **arXiv API** using a keyword-based query.
- Extract and store metadata including title, abstract, and PDF URL in a structured CSV.

#### **2. Document Embedding**
- Use **sentence-transformers/all-MiniLM-L6-v2** to generate vector embeddings from each abstract.  
- Store embeddings in a **FAISS index** for efficient semantic retrieval.

#### **3. Retrieval & Ranking**
- **Retrieval**: Given a user query (can be different from the original scrape keyword), find the most semantically similar abstracts from FAISS.  
- **Ranking**: Use **SciBERT** (trained on scientific data) to score and sort the top results based on relevance to the query.

#### **4. Summarization**
- The top 3 ranked papers are passed through a **LangChain-based RetrievalQA pipeline** using **Ollama (LLaMA 3.2)**.  
- Each result is returned with:
  - Paper title  
  - PDF link  
  - Abstract  
  - Generated summary

#### **5. Output Saving**
- Final results are saved into:
  - **Markdown file** (`top_summarized_papers.md`)

---

### **Future Enhancements**
- Add support for downloading and parsing full paper PDFs using the arXiv `pdf_url`.
- Enable contradiction or claim-matching by comparing current statements with past publications (e.g., fake statement detection).
- Support additional academic sources (PubMed, IEEE Xplore).
- Build a Streamlit UI for interactive querying and visualization.

---

### **License**
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
