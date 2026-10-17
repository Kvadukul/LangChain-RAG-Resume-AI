# LangChain RAG Resume AI Agent

An automated Retrieval Augmented Generation (RAG) pipeline built as an AI powered Assistant to ingest, chunk, and input candidate PDF resumes.

---

## Agent Breakdown

| Library | Purpose & Implementation |
| :--- | :--- |
| **`PyPDFDirectoryLoader`** | Loads all the PDFs from the specified folder so the script can use the whole directory at once. |
| **`RecursiveCharacterTextSplitter`** | Splits the data (PDFs/CVs) into smaller sections so relative info is found quicker. |
| **`Chroma` & Embeddings** | Stores splits and calculations; converts text into specialised code/embeddings via Gemini so the AI understands it. |
| **`ChatGoogleGenerativeAI`** | Connects Gemini (gemini-3.8-flash) to the code (temperature=0 to ensure no excess info is printed). |
| **`ChatPromptTemplate`** | Formats the prompt containing context (relevant data chunks) and input (user question). |
| **`format_docs`** | Helper function checking Chroma storage, grabbing text from chunks, and joining lists of texts back into readable sentences. |
| **`RunnablePassthrough` & `StrOutputParser`** | Handles inputs sent into the chain and converts Gemini responses back into text format. |

---

## Tuning of K

I increased the retriever limit to k=20 because a lower setting like 5 didn't pull enough information. Even though I thought a higher k might slow things down, it actually lets the system search a wider net and bring much more evidence to the AI, which is really helpful when you are looking at multiple cv's with similar details across multiple documents.

## Issues Found

I ran into issues when asking overly broad questions like trying to get a list of everyone's names or a full summary of all CVs because RAG isn't built for reading everything. It targets specific keywords, job experiences, and skills first. While you could technically make k massively huge ( like k = 200) to try and capture everything, it would become way too slow and completely inefficient.
