# 💍 Spousal Approval System

A multi-agentic, multi-modal Streamlit application that evaluates your ideas before you present them to your spouse. Built for portfolio demonstration.

---

## Architecture

```
User Voice Input
      │
      ▼
[Agent 1: Groq Whisper]
  Speech → Text Transcription
      │
      ▼
[Review Stage]
  User edits / confirms transcript
      │
      ▼
[Agent 2: Groq LLaMA-3.3-70b]
  Idea Severity Scoring (1–10)
      │
      ├── Score ≤ 2 ──────────────► ✅ SAFE — No action needed
      │
      ├── Score 3–7 ──────────────► ⚠️ SPOUSE AGENT
      │                               Calm but firm disapproval
      │                               + TTS voice response (gTTS)
      │                                     │
      │                               User submits anyway?
      │                                     ▼
      │                              💥 SPOUSE RAGE MODE
      │
      └── Score 8–10 ─────────────► 📱 FRIEND INTERVENTION AGENT
                                      Urgent friendly warning call
                                      + TTS voice (different accent)
                                            │
                                      User submits anyway?
                                            ▼
                                     💥 SPOUSE RAGE MODE
                                            │
                                      User argues back?
                                            ▼
                                     🧳 EXILE MODE (20s lockout)
```

## Stack

| Layer | Technology |
|-------|-----------|
| Framework | Streamlit |
| Speech-to-Text | Groq Whisper Large v3 |
| LLM Evaluation | Groq LLaMA-3.3-70b-versatile |
| Text-to-Speech | gTTS (Google TTS) |
| Styling | Custom CSS (Playfair Display + Crimson Pro) |

## Setup

### 1. Install dependencies
```bash
pip install -r requirements.txt
```

### 2. Set your Groq API key

**Option A: Environment variable**
```bash
export GROQ_API_KEY="your_key_here"
```

**Option B: Streamlit secrets**
Create `.streamlit/secrets.toml`:
```toml
GROQ_API_KEY = "your_key_here"
```

Get a free Groq API key at: https://console.groq.com

### 3. Run the app
```bash
streamlit run app.py
```

---

## Features

- 🎙️ **Voice input** via Streamlit's built-in `st.audio_input` or file upload
- 📝 **Editable transcript** review before submission
- ⚖️ **AI severity scoring** with JSON-structured output
- 🗣️ **Three distinct AI agents**: Spouse (calm), Spouse (rage), Friend
- 🔊 **Text-to-speech** voice responses with different accents per character
- 🧳 **Exile mode**: 20-second lockout with countdown after repeated bad decisions
- 🎨 **Luxury dark aesthetic** with gold accents, serif typography, and micro-animations

---

## Agent Prompting Strategy

Each agent uses a distinct persona and tone:

**Scoring Agent**: Structured JSON output, calibrated 1-10 scale with routing thresholds  
**Spouse Agent (calm)**: 3-4 sentences, "calm but disappointed", reasoning-based  
**Friend Agent**: Warm, urgency-coded, avoids clichés ("Hey buddy"), mid-conversation entry  
**Spouse Agent (rage)**: "Absolutely furious and appalled", dramatic, 4-5 sentences

---

*No marriages were harmed in the making of this application.*
