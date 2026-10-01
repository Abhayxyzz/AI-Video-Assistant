# 🎬 AI Video Assistant

Turn any meeting recording or YouTube video into a searchable, summarized knowledge base — then chat with it.

Paste a YouTube link or point it at a local file, pick a language, and it transcribes, summarizes, extracts key information, and lets you ask follow-up questions grounded in the transcript.

## How It Works

```
YouTube URL / Local File
        ↓
  Audio Processing (download / convert / chunk)
        ↓
   Transcription (Whisper · English | Sarvam AI · Hinglish)
        ↓
  ┌─────────────┬──────────────┬─────────────┐
  Summarization   Extraction     RAG Indexing
  (map-reduce)   (action items,  (ChromaDB +
                  decisions,      embeddings)
                  questions)
        ↓
   Streamlit dashboard + chat with the meeting
```

## Features

- 🎙️ **Transcription** of YouTube videos or local audio/video files, with support for English (Whisper) and Hinglish (Sarvam AI speech-to-text-translate)
- 📝 **Summarization** of long transcripts using a map-reduce approach, so even hour-long meetings stay digestible
- ✅ **Extraction** of action items, key decisions, and open questions as separate structured outputs
- 💬 **RAG chat** to ask questions about the meeting, with answers grounded only in the transcript
- 🖥️ **Streamlit UI** with live pipeline status and a results dashboard (summary, transcript, extracted items, chat)
- 🧱 **Modular design** — every stage (audio, transcription, summarization, extraction, retrieval) is a separate, swappable component

## Project Structure

```
├── Audio_Processor.py   # Downloads/converts input and chunks audio
├── Transcriber.py       # Routes audio to Whisper or Sarvam AI
├── Summarizer.py        # Map-reduce summarization + title generation
├── Extractor.py         # Extracts action items, decisions, open questions
├── Vector_Store.py      # Builds/loads the Chroma vector store
├── Rag_Engine.py        # RAG chain for chatting with the transcript
├── Main.py              # CLI entry point, runs the full pipeline
└── App.py               # Streamlit web app
```

## Getting Started

```bash
# 1. Clone the repo
git clone <your-repo-url>
cd <your-repo-name>

# 2. Install dependencies
pip install -r requirements.txt

# 3. Add required keys to a .env file
GROQ_API_KEY=your_key_here
SARVAM_API_KEY=your_key_here   # only needed for Hinglish transcription

# 4a. Run the web app
streamlit run App.py

# 4b. Or run from the terminal
python Main.py
```

> **Note:** `ffmpeg` is required for audio conversion (used by `pydub` and `yt-dlp`). Install it separately if it's not already on your system.

## Tech Stack

Python · LangChain · Whisper · Sarvam AI · ChromaDB · HuggingFace Embeddings · Groq · yt-dlp · Streamlit

## Roadmap

- [ ] Speaker diarization, to tie action items to specific people
- [ ] Support for more languages beyond English and Hinglish
- [ ] Export summary and action items as a shareable report

## License

MIT
