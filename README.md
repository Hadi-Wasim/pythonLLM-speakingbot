# 🗣️🎧 AI Voice Assistant Chatbot

### **Real-Time Speech-to-Text + Text-to-Speech Conversational AI Using IBM Watson & OpenAI Models**

This repository contains an end-to-end **voice-enabled AI chatbot system** that integrates:

* **IBM Watsonx Speech-to-Text (STT)**
* **IBM Watsonx Text-to-Speech (TTS)**
* **OpenAI GPT-5-nano** for language generation
* **Flask REST API Backend**
* **Modern HTML/CSS/JavaScript Frontend**

The application enables **full-duplex voice interaction**, converting user speech → text → LLM response → synthesized speech, all inside a seamless web interface.

---

# 🚀 Features

### 🎙️ **1. Real-Time Speech Recognition (IBM Watson STT)**

* High-fidelity ASR (Automatic Speech Recognition)
* Multimedia-optimized acoustic model: `en-US_Multimedia`
* Audio submitted as binary streams
* Robust transcription using HTTP POST API

### 🧠 **2. Natural Language Understanding (OpenAI GPT-5-nano)**

The assistant:

* Understands user queries
* Answers, summarizes, translates, or recommends
* Obeys a concise system prompt
* Uses OpenAI’s **chat.completions** endpoint

### 🔊 **3. Neural Text-to-Speech (IBM Watson TTS)**

* Generates WAV audio output
* Supports dynamic voice selection
* Low-latency synthesis using REST API

### 🌐 **4. Full Frontend Architecture (HTML/CSS/JS)**

Includes:

* Microphone recording via Web Audio API
* Fetch-based networking
* Dynamic DOM rendering of responses
* Auto-playback of synthesized speech

### 🧩 **5. Flask Backend (Python)**

Microservice architecture:

* `/speech-to-text` → Watson STT
* `/process-message` → OpenAI LLM + Watson TTS
* JSON + Base64 encoded audio payloads
* CORS enabled

---

# 🏗️ System Architecture

```
               ┌───────────────────────────────────────────┐
               │                 FRONTEND                   │
               │  HTML + CSS + JS                           │
               │  - Voice Recording                         │
User ───────▶  │  - JSON Requests                           │
(Microphone)    │  - Audio Playback                         │
               └───────────────────────────────────────────┘
                               │
                               ▼
               ┌───────────────────────────────────────────┐
               │                 FLASK API                  │
               │  server.py                                 │
               │  - /speech-to-text                         │
               │  - /process-message                        │
               └───────────────────────────────────────────┘
                      │                    │
         ┌────────────┘                    └──────────────┐
         ▼                                                 ▼
┌─────────────────────┐                         ┌──────────────────────────┐
│  IBM Watson STT     │                         │      OpenAI GPT-5-nano  │
│  Speech → Text       │                         │  Text Generation         │
└─────────────────────┘                         └──────────────────────────┘
                                                               │
                                                               ▼
                                              ┌──────────────────────────┐
                                              │    IBM Watson TTS        │
                                              │    Text → Speech (WAV)   │
                                              └──────────────────────────┘
                                                               │
                                                               ▼
                                                    Audio returned to user
```

---

# 📁 Project Structure

```
.
├── server.py          # Flask backend server
├── worker.py          # Core logic: STT, TTS, LLM
├── static/            # CSS, images, JS
├── templates/
│   └── index.html     # Frontend UI
├── requirements.txt   # Python dependencies
└── README.md          # Project documentation
```

---

# 🧪 API Endpoints

## 🎤 `POST /speech-to-text`

Input:

* Binary audio stream (`audio/wav`, `audio/webm`)

Output:

```json
{
  "text": "recognized transcript"
}
```

## 💬 `POST /process-message`

Input:

```json
{
  "userMessage": "What is the weather?",
  "voice": "en-US_AllisonV3Voice"
}
```

Response:

```json
{
  "openaiResponseText": "Here is the concise reply...",
  "openaiResponseSpeech": "<base64_encoded_audio>"
}
```

---

# ⚙️ Tech Stack

### **Backend**

* Python 3.x
* Flask
* IBM Watsonx REST APIs
* OpenAI API
* Requests library

### **Frontend**

* HTML5
* Tailored CSS
* Vanilla JavaScript
* Fetch API
* Web Audio API

---

# 🔧 Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/voice-chatbot.git
cd voice-chatbot
```

### 2. Create virtual environment

```bash
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up API keys

Inside `worker.py`, configure:

* IBM Watson STT endpoint
* IBM Watson TTS endpoint
* OpenAI API key

### 5. Run the server

```bash
python server.py
```

Visit:
👉 **[http://localhost:8000](http://localhost:8000)**

---

# 📡 Networking & Transport Layer Notes

* Audio over HTTP transported as binary octet-stream
* Post-processing uses Base64 encoding for client compatibility
* CORS enabled for cross-origin frontend integrations
* Asynchronous REST design pattern
* Stateless, idempotent endpoints

---

# 🔥 Advanced Concepts Used

* **Acoustic Modeling** (Watson STT)
* **Neural Vocoders** (Watson TTS)
* **Large Language Model Inference (OpenAI GPT-5-nano)**
* **Prompt Engineering** for deterministic response behavior
* **Browser-side audio capture** using Web Media API
* **Multimodal serialization** (Base64 audio payloads)
* **Microservice-oriented backend architecture**

---

# 📈 Future Enhancements (Planned Roadmap)

* Add conversation memory
* Add multilingual models
* Add Gemini / Claude 3 backends
* Add streaming audio response
* Use WebSockets for real-time interaction

---

# 🤝 Contributing

Pull requests are welcome.
For major changes, open an issue first to discuss the proposal.

---

