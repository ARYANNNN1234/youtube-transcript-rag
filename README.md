# 🎥 YouTube Transcript RAG Assistant

Ask questions about any YouTube video using its transcript.

This project uses Retrieval-Augmented Generation (RAG) to fetch a video's transcript, convert it into embeddings, store them in a vector database, and answer questions grounded in the transcript.

The project includes two interfaces:

- **Streamlit Web App** – quick local UI for interacting with transcripts.
- **Chrome Extension** – ask questions directly while watching a YouTube video.

---

## 🚀 Features

- Extract transcript from YouTube videos
- Chunk transcript and create embeddings
- Store vectors using FAISS
- Perform semantic search
- Generate answers using Groq LLM (Llama-3.3-70B)
- Ask questions about any part of the video
- Chrome extension automatically detects the current YouTube video
- Streamlit UI for standalone usage

---
## 🧠 Architecture
                ┌─────────────────────────┐
                │      YouTube Video      │
                └────────────┬────────────┘
                             │
                             ▼
                 YouTube Transcript API
                             │
                             ▼
               Transcript Chunking (LangChain)
                             │
                             ▼
                  Embeddings (MiniLM Model)
                             │
                             ▼
                     FAISS Vector Store
                             │
                             ▼
                    Semantic Retrieval
                             │
                             ▼
                     Groq LLM (Llama)
                             │
                             ▼
                      Generated Answer
                      



---

## 📂 Project Structure
youtube-transcript-rag/ │ ├── backend/ │ ├── app.py # FastAPI backend for Chrome extension │ ├── requirements.txt │ └── .env # API keys (not committed) │ ├──  app.py # Streamlit interface │ ├── extension/ │ ├── manifest.json │ ├── service-worker.js │ ├── content.js │ ├── sidepanel.html │ ├── sidepanel.js │ └── sidepanel.css │ └── README.md

---

## ⚙️ Installation

**Clone the repository:**

```bash
git clone https://github.com/yourusername/youtube-transcript-rag.git
cd youtube-transcript-rag
```

## Create a virtual environment:
```bash
python -m venv venv
```
## Activate the environment:

**Windows:**
```bash
venv\Scripts\activate
```
**Mac/Linux:**
```bash
source venv/bin/activate
```
## 📦 Install Dependencies

Install the required Python packages:

```bash
pip install -r backend/requirements.txt
```

---

## 🔑 Environment Variables

Create a `.env` file inside the **backend** folder:

```env
GROQ_API_KEY=your_groq_api_key
```

Get your API key from:  
https://console.groq.com/

---

## 💻 Running the Streamlit App

The Streamlit interface allows you to ask questions about a YouTube video locally.

Run the Streamlit app:

```bash
streamlit run streamlit_app/app.py
```

Open your browser at:

```
http://localhost:8501
```

Then:

1. Enter the **YouTube video ID**
2. Enter the **transcript language**
3. Ask questions about the video

---

## 🔌 Chrome Extension Setup

The Chrome extension lets you ask questions **while watching a video on YouTube**.

---

### Step 1 — Run Backend API

Start the FastAPI backend:

```bash
cd backend
uvicorn app:app --reload --port 8000
```

Verify the backend is running:

```
http://127.0.0.1:8000/health
```

---

### Step 2 — Load Chrome Extension

1. Open **Google Chrome**
2. Go to:

```
chrome://extensions
```

3. Enable **Developer Mode**
4. Click **Load Unpacked**
5. Select the `extension` folder

---

### Step 3 — Use the Extension

1. Open any **YouTube video**
2. Click the **extension icon**
3. The **side panel opens**
4. Enter a question
5. Click **Ask**

The extension will:

- Detect the current **video ID**
- Send it to the **backend**
- Retrieve transcript context
- Generate an answer using **Groq**

---

## 🌐 Deploying Backend (Render)

To make the extension usable outside your local machine, deploy the backend.

### 1️⃣ Push the repository to GitHub

### 2️⃣ Create a **Render Web Service**

Use the following commands:

**Build Command**

```bash
pip install -r requirements.txt
```

**Start Command**

```bash
uvicorn app:app --host 0.0.0.0 --port $PORT
```

Add environment variable:

```
GROQ_API_KEY=your_key
```

Render will provide a public API URL, for example:

```
https://youtube-rag.onrender.com
```

Update `extension/service-worker.js`:

```javascript
fetch("https://your-render-url/ask")
```

---

## 📊 Technologies Used

- Python
- FastAPI
- Streamlit
- LangChain
- FAISS
- HuggingFace Embeddings
- Groq LLM
- YouTube Transcript API
- Chrome Extension API

---

## 📌 Example Usage

Ask questions like:

- **What is the main topic of this video?**
- **Summarize the key ideas discussed.**
- **What are the important concepts explained at the end?**

The system retrieves relevant transcript chunks and generates grounded answers.
