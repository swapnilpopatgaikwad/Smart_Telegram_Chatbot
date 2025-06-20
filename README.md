
# 🤖 Smart Telegram Chatbot (AI-Powered Auto-Responder)

This project is an **n8n workflow** that turns your **Telegram bot into an AI voice assistant**. It listens to voice messages from Telegram users, transcribes them into text, processes the text using **Google Gemini AI**, and sends back intelligent responses in real-time.

---

## 📌 Features

- ✅ Telegram bot trigger to listen for incoming voice messages  
- ✅ Fetch voice file and transcribe it using **SpeakNotes API**  
- ✅ AI-powered response using **Google Gemini (PaLM)**  
- ✅ Sends reply back via Telegram automatically  
- ✅ Fully automated and can be run on any self-hosted n8n instance  

---

## 🔗 Workflow Architecture

```mermaid
graph TD
  A[Telegram Trigger] --> B[Get Audio File Details]
  B --> C[Fetch Audio File]
  C --> D[Convert Audio to Transcription (SpeakNotes API)]
  D --> E[AI Agent]
  E --> F[Telegram Send Message]
  subgraph AI Integration
    E --> G[Google Gemini Chat Model]
  end
```

---

## ⚙️ Requirements

- A **Telegram Bot Token**  
- A **SpeakNotes API key** for transcription  
- A **Google Gemini (PaLM) API key**  
- Self-hosted or cloud n8n instance  

---

## 🧠 How It Works

1. **User sends voice message** to Telegram bot.
2. Bot **fetches file ID** and then **downloads** the voice file using Telegram API.
3. Audio is **uploaded to SpeakNotes API** for transcription.
4. The transcribed text is passed to **Gemini AI** using LangChain integration.
5. Gemini returns a smart reply which is **sent back to the user** on Telegram.

---

## 🔐 Credential Setup in n8n

### 1. **Telegram API**
- Add a new credential in n8n named: `Smart Telegram Chatbot (AI-Powered Auto-Responder)`
- Use your **Telegram bot token**

### 2. **Google Gemini API**
- Create under `Google PaLM API`
- Set credential name: `Google Gemini(PaLM) Api account`

---

## 📂 Nodes Used

| Node Name                   | Type                        | Description                                   |
|----------------------------|-----------------------------|-----------------------------------------------|
| Telegram Trigger           | `telegramTrigger`           | Listens for voice messages                    |
| Get Audio File Details     | `httpRequest`               | Calls `getFile` API to get file path          |
| Featch Audio File          | `httpRequest`               | Downloads voice file using the file path      |
| Convert Audio to Text      | `httpRequest`               | Uploads file to SpeakNotes for transcription  |
| AI Agent                   | `LangChain Agent`           | Processes transcription using Gemini          |
| Google Gemini Chat Model   | `LangChain: Gemini`         | Gemini LLM chat model                         |
| Telegram Reply             | `telegram`                  | Sends response back to the user               |

---

## 🧪 Test Data (Example)

**Voice Input (Ogg):**  
Transcription: `you create a hello program in C sharp`  
**AI Output:**  
> “Sure! Here's a simple Hello World program in C#...”

---

## 🚀 Deployment

You can deploy this workflow on:

- 🐳 Docker-based n8n self-hosted instance  
- 🧩 n8n cloud instance  
- 🖥️ Local development for testing  

---

## 📌 Notes

- The Telegram Bot must be set to **allow voice messages**
- SpeakNotes API returns transcription in English (other languages may vary)
- All APIs must be authenticated in the **n8n credentials section**

---

## 📝 License

MIT License  
© 2025 Your Name or Company
