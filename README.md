Ask This Page 🤖

A full-stack AI Chrome Extension that turns any webpage, YouTube video, or PDF into a conversational chatbot. This is a personal portfolio project.

---


## 🚀 Features#

* **Chat with Webpages:** Scrapes and processes any static webpage to answer your questions.
* **Chat with YouTube:** Fetches and translates non-English video transcripts to provide answers.
* **Chat with PDFs:** Reads any public PDF file from a URL and lets you chat with it.
* **AI Chat Memory:** Remembers your conversation history for follow-up questions.
* **One-Click Prompts:** Buttons for common tasks like "Summarize" and "List Key Topics."
* **Markdown Rendering:** Displays the AI's formatted answers (bullet points, bold) correctly.
* **Copy to Clipboard:** Easily copy any AI response.

---

## 🛠️ Tech Stack

This project is a **monorepo** with two main parts:

* **Frontend (Chrome Extension):**
    * HTML5
    * CSS3
    * JavaScript (ES6+)
    * `marked.js` (for Markdown rendering)
    * Chrome Extension Manifest V3 API

* **Backend (Python API Server):**
    * **Framework:** Flask (with Flask-CORS)
    * **AI/LangChain:**
        * `langchain`
        * Google Gemini Pro (`gemini-2.5-flash`)
        * Google Embeddings (`models/embedding-001`)
    * **Vector Store:** `faiss-cpu` (for in-memory semantic search)
    * **Data Loaders:**
        * `beautifulsoup4` (for HTML)
        * `youtube-transcript-api` (for YouTube)
        * `pypdf` & `requests` (for PDFs)

---

## 🏗️ How It Works: Architecture

1.  The **Chrome Extension (Frontend)** is activated on a page.
2.  It detects the content type (Webpage, YouTube, PDF) and sends the data (HTML, Video ID, or PDF URL) to the **Flask (Backend)**.
3.  The backend **processes** the data: it cleans it, splits it into chunks, and uses Google's Embedding model to turn the chunks into vectors.
4.  These vectors are stored in a `FAISS` **vector store** in the server's memory.
5.  When the user asks a question, the backend uses **LangChain's `ConversationalRetrievalChain`** to:
    a. Find the most relevant chunks from the vector store (RAG).
    b. Pass the context, chat history, and new question to the **Gemini LLM**.
6.  Gemini generates an answer, which is sent back to the extension and displayed.

---

## 🏁 How to Run This Locally

### Prerequisites

* [Python 3.9+](https://www.python.org/downloads/)
* [Google AI Studio API Key](https://aistudio.google.com/app/apikey)
* A Chrome-based browser

### 1. Backend Setup

First, let's get the Python server running.

```bash
# 1. Clone this repository
git clone [https://github.com/YOUR_USERNAME/ask-this-page.git](https://github.com/YOUR_USERNAME/ask-this-page.git)
cd ask-this-page/backend

# 2. Create and activate a virtual environment
python -m venv venv
# On Windows:
.\venv\Scripts\Activate
# On Mac/Linux:
source venv/bin/activate

# 3. Install all required packages
pip install -r requirements.txt

# 4. Create your environment file
# Create a new file named ".env" in the /backend folder
# Add your API key to this file:
GOOGLE_API_KEY="YOUR_API_KEY_HERE"

# 5. Run the server!
python app.py


2. Frontend (Chrome Extension) Setup


Open your Chrome browser.

Go to the extensions page by typing chrome://extensions in the address bar.

In the top-right corner, turn on "Developer mode".

Click the "Load unpacked" button that appears.

In the file dialog, select your ENTIRE frontend folder.

The "Ask This Page" extension will appear. You can now use it!
