# My Low-Code AI Chatbot in UET

This project demonstrates how to build a **low-code AI chatbot** using:

* 🌀 **n8n**: Low-code workflow engine.
* 🤖 **Ollama + Mistral-7B**: AI-powered text generation.
* 🔎 **Elasticsearch**: Data storage and search.
* 💬 **Telegram**: Chat interface.

The chatbot crawls articles from `insideHPC.com`, summarizes them with AI, indexes them into Elasticsearch, and allows users to query via Telegram with real-time responses.

---

## 📂 Project Structure

| Folder/File    | Description                                    |
| -------------- | ---------------------------------------------- |
| `/workflow/`   | Contains exported n8n workflow files.          |
| `/report/`     | PDF report and LaTeX source.                   |
| `README.md`    | Project documentation (this file).             |

---

## 🚀 Quick Start

### 1️⃣ Self-hosting

You'll need:

| Tool          | Version (suggested)                 |
| ------------- | ----------------------------------- |
| n8n           | >= 1.0                              |
| Elasticsearch | >= 8.x (Cloud or Local)             |
| Ollama        | Installed locally (with Mistral-7B) |
| ngrok         | (for tunneling, optional)           |
| Telegram Bot  | (created via @BotFather)            |

👉 **Example install:**

```bash
# Install n8n
npm install n8n -g

# Install ngrok
# (Skip if you have your own domain)
brew install ngrok  # or download manually

# Elasticsearch (Cloud or Docker)
docker run -p 9200:9200 -e "discovery.type=single-node" elasticsearch:8.11.0
```

---

### 2️⃣ Set Up n8n

* Run n8n:

```bash
n8n
```

* Import the workflow files (`workflow/`) using n8n UI.

* Update these nodes:

  * **Elasticsearch nodes**: configure with your Elasticsearch URL + credentials.
  * **Ollama API**: set up the model (Mistral-7B).
  * **Telegram nodes**: paste your Bot Token.

---

### 3️⃣ Expose n8n to Telegram (Webhook)

**Option 1: Using Ngrok (quickest)**

```bash
ngrok http 5678
```

Copy the HTTPS URL from ngrok, e.g., `https://abcd1234.ngrok.io`.

Set webhook for Telegram:

```bash
curl -X POST "https://api.telegram.org/bot<YOUR_BOT_TOKEN>/setWebhook?url=https://abcd1234.ngrok.io/webhook/telegram"
```

**Option 2: Own Domain + Reverse Proxy**

* Set up a domain and point it to your server.
* Use Nginx or Caddy to proxy to `localhost:5678`.
* Make sure it's HTTPS!

---

### 4️⃣ Run the Chatbot

* **Workflow 1:** Crawl and summarize articles.
* **Workflow 2:** Chatbot receives messages and responds via Telegram.

✅ Now test it: send `/start` or any message to your Telegram bot!

---

## 💡 Example Commands

| Command                 | Description                                         |
| ----------------------- | --------------------------------------------------- |
| `/start`                | Initiates chat with the bot.                        |
| Ask: "Latest HPC news?" | The bot fetches from Elasticsearch + AI generation. |

---

## 📝 Configuration Notes

* **Ollama**: Ensure Mistral-7B is downloaded locally.
* **Elasticsearch**: Cloud recommended for production; local works for testing.
* **n8n Webhook URL**: Must be HTTPS (Telegram requires it).

---

## 🙌 Credits

* **Student**: Ngo Van Kiet - 22022643
* **Advisor**: Ph.D Nguyen Viet Cuong

---

## 🔗 Useful Links

* [n8n Documentation](https://docs.n8n.io/)
* [Ollama](https://ollama.com/)
* [Elasticsearch Docs](https://www.elastic.co/guide/en/elasticsearch/)
* [Telegram Bot API](https://core.telegram.org/bots/api)

---

## 🚀 Contact
Feel free to send me any questions about launching this project through my email **kietngo9204@gmail.com**
