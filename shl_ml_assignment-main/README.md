# SHL Conversational Assessment Recommendation System

**Author:** Rachit Saxena

A modern, AI-driven assistant for recommending SHL assessments using conversational context, vector search, and grounded generation.

![Postman API Demo](assets/postman-demo.png)

> Example request flow: user asks for hiring recommendations, the assistant asks clarifying questions, and returns grounded assessment guidance.

---

## 🚀 Key Features

- **Conversational recommendation engine** with follow-up questions
- **Hybrid retrieval** using FAISS vector search + metadata reranking
- **Grounded answers** with reduced hallucination risk
- **Senior-level awareness** for role-specific suggestions
- **Strict JSON output** for API-friendly integration

---

## 💡 What This Project Does

This app helps recruiters and hiring teams:

- recommend technical, personality, and cognitive assessments
- refine recommendations across multiple conversation turns
- balance between skill-based and behavioral assessment needs
- keep chat history stateless using `messages[]`

---

## 🧠 Technology Stack

- Python
- FastAPI
- Google Gemini API
- FAISS vector search
- Sentence Transformers
- Uvicorn

---

## 📁 Project Structure

```bash
.
├── app.py
├── semantic_rag.py
├── retriever.py
├── prompts.py
├── conversation.py
├── create_index.py
├── normalize_data.py
├── requirements.txt
├── .env
├── README.md
├── assets/
│   └── postman-demo.png
├── data/
│   ├── catalog.json
│   ├── normalized_assessments.json
│   ├── faiss.index
│   ├── embeddings.npy
│   └── shl.db
```

---

## 🛠️ Setup Instructions

### 1. Clone the repository

```bash
git clone <your_repo_url>
cd <repo_name>
```

### 2. Create and activate a virtual environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🔑 Environment Variables

Create a `.env` file with your Gemini API key:

```env
Gemini_API_Key=YOUR_GEMINI_API_KEY
```

---

## 📦 Data Preparation

1. Place the SHL catalog dataset in `data/catalog.json`
2. Run normalization:

```bash
python normalize_data.py
```

3. Create the FAISS index:

```bash
python create_index.py
```

---

## ▶️ Run the API

```bash
uvicorn app:app --reload
```

Open the app at:

```bash
http://127.0.0.1:8000
```

Explore docs at:

- `http://127.0.0.1:8000/docs`
- `http://127.0.0.1:8000/redoc`

---

## 📡 API Reference

### POST `/chat`

Send a JSON body with `messages`:

```json
{
  "messages": [
    {"role": "user", "content": "I am hiring a Java developer. Can you recommend some assessments?"}
  ]
}
```

Response example:

```json
{
  "reply": "What seniority level are you hiring for?",
  "recommendations": [],
  "end_of_conversation": false
}
```

---

## ⭐ Notes

- The assistant is designed to ask clarifying questions before final recommendations.
- It uses the SHL catalog and embeddings to ground advice.
- If you want the screenshot shown here, save your demo image as `assets/postman-demo.png`.

### Request

```json
{
  "messages": [
    {
      "role": "user",
      "content": "Hiring Java backend developer"
    },
    {
      "role": "assistant",
      "content": "What seniority level?"
    },
    {
      "role": "user",
      "content": "Mid-level and needs teamwork skills"
    }
  ]
}
```

---


---

### Example Response

```json
{
  "reply": "For a mid-level Java backend developer, I recommend using the 'Core Java (Advanced Level) (New)' assessment to gauge technical proficiency.",
  "recommendations": [
    {
      "name": "Core Java (Advanced Level) (New)",
      "url": "https://www.shl.com/products/product-catalog/view/core-java-advanced-level-new/",
      "test_type": "Technical"
    }
  ],
  "end_of_conversation": true
}
```

---

# Retrieval Pipeline

The retrieval pipeline performs:

1. Semantic FAISS retrieval
2. Metadata-aware reranking
3. Technical/personality balancing
4. Seniority-aware boosting
5. Noise filtering
6. Diversity enforcement

---

# Deployment (Render)

## Build Command

```bash
pip install -r requirements.txt
```

---

## Start Command

```bash
uvicorn app:app --host 0.0.0.0 --port $PORT
```

---

## Environment Variable

Add in Render dashboard:

```env
Gemini_API_Key=YOUR_GEMINI_API_KEY
```

---

# Notes

- Uses precomputed FAISS embeddings for faster startup
- Optimized for CPU-only deployment
- Supports Render free tier deployment
- Uses Gemini API instead of local LLMs for lower memory usage

---

# Future Improvements

- Better metadata enrichment
- Hybrid SQL + vector retrieval
- Persistent conversation analytics
- Advanced evaluation metrics
- Frontend UI
- Docker support

---
## 👤 Author

**Name:** Rachit Saxena  
**LinkedIn:** [https://www.linkedin.com/in/rachit-saxena-5a8794397/](https://www.linkedin.com/in/rachit-saxena-5a8794397/)  
**GitHub:** [https://github.com/Rachit2982](https://github.com/Rachit2982)  
**Email:** rachitsaxena12345433@gmail.com


# License

MIT License