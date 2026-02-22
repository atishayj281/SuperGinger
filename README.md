# 🫚 SuperGinger

> A private, AI-powered chatbot for personalised document conversations — built on Microsoft Bot Composer and powered by Ollama.

![GitHub repo size](https://img.shields.io/github/repo-size/atishayj281/SuperGinger)
![GitHub stars](https://img.shields.io/github/stars/atishayj281/SuperGinger?style=social)
![GitHub forks](https://img.shields.io/github/forks/atishayj281/SuperGinger?style=social)
![License](https://img.shields.io/github/license/atishayj281/SuperGinger)
![Platform](https://img.shields.io/badge/platform-Microsoft%20Bot%20Composer-blue)
![AI](https://img.shields.io/badge/AI-Ollama-orange)
![.NET](https://img.shields.io/badge/.NET-C%23-purple)

---

## 📋 Table of Contents

- [About](#about)
- [Features](#features)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Privacy & Security](#privacy--security)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 📖 About

**SuperGinger** is a fully private, AI-powered chatbot that lets you have natural, intelligent conversations with your own documents. Whether it's PDFs, reports, manuals, or internal knowledge bases — SuperGinger understands your content and answers your questions accurately, without sending your data to any third-party cloud.

Built on top of **Microsoft Bot Composer** for the conversational interface and **Ollama** for running large language models (LLMs) locally, SuperGinger ensures that your documents and conversations stay completely on your machine.

---

## ✨ Features

- 🔒 **100% Private** — All AI inference runs locally via Ollama; no data leaves your system
- 📄 **Document-Aware Conversations** — Chat with your own documents stored in the knowledge base
- 🤖 **Personalised Responses** — Context-aware answers grounded in your specific documents
- 🧠 **Powered by Local LLMs** — Leverages Ollama to run models like LLaMA, Mistral, Gemma, and more
- 🎨 **No-Code Bot Design** — Built with Microsoft Bot Composer for an easy-to-extend dialog flow
- ⚡ **Fast Local Inference** — No API latency; runs entirely on your hardware
- 🔧 **Customisable** — Swap AI models or extend dialogs without rewriting core logic

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     User Interface                      │
│              (Bot Composer Web Chat / Teams)             │
└───────────────────────┬─────────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────────┐
│              Microsoft Bot Composer                      │
│     (Dialogs, Recognizers, Language Understanding)       │
└───────────────────────┬─────────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────────┐
│              ASP.NET Core Bot Runtime                    │
│          (Program.cs / Startup.cs / Controllers)         │
└───────────────────────┬─────────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────────┐
│                  Knowledge Base                          │
│          (Local document store for Q&A context)          │
└───────────────────────┬─────────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────────┐
│                     Ollama (Local)                       │
│         (LLM Inference — LLaMA / Mistral / etc.)         │
└─────────────────────────────────────────────────────────┘
```

All components run locally on your machine — zero cloud dependency.

---

## 🚀 Getting Started

### Prerequisites

Ensure the following are installed on your system before proceeding:

| Tool | Version | Purpose |
|---|---|---|
| [Ollama](https://ollama.com/) | Latest | Local LLM inference |
| [Microsoft Bot Framework Composer](https://aka.ms/bf-composer-download) | Latest | Bot dialog authoring |
| [.NET SDK](https://dotnet.microsoft.com/download) | 6.0+ | ASP.NET Core bot runtime |
| [Node.js](https://nodejs.org/) | v16+ | Bot Composer dependencies |
| Git | Any | Cloning the repository |

### Installation

#### 1. Clone the Repository

```bash
git clone https://github.com/atishayj281/SuperGinger.git
cd SuperGinger
```

#### 2. Set Up Ollama

Install Ollama from [https://ollama.com](https://ollama.com) and pull your preferred model:

```bash
# Pull a model of your choice
ollama pull llama3
# or
ollama pull mistral
# or
ollama pull gemma
```

Start the Ollama server:

```bash
ollama serve
```

> By default, Ollama runs on `http://localhost:11434`. Make sure it's running before launching the bot.

#### 3. Restore .NET Dependencies

```bash
cd Super_Ginger
dotnet restore
```

#### 4. Configure Settings

Update the bot settings in the `settings/` directory with your Ollama endpoint and preferred model:

```json
{
  "OllamaBaseUrl": "http://localhost:11434",
  "OllamaModel": "llama3"
}
```

#### 5. Open in Bot Composer

- Launch **Microsoft Bot Framework Composer**
- Click **Open** and select the `Super_Ginger.botproj` file
- The bot project will load with all dialogs, recognizers, and language settings

#### 6. Add Your Documents

Place your documents inside the `knowledge-base/` folder. These will be used as context for AI-powered responses.

#### 7. Run the Bot

```bash
dotnet run
```

Or use the **Start Bot** button directly within Bot Composer.

---

## 🛠️ Usage

### Adding Your Documents

Place your documents in the `knowledge-base/` folder:

```bash
cp your-document.pdf ./Super_Ginger/knowledge-base/
```

### Chatting with Your Documents

1. Open the **Bot Composer Web Chat** panel (or connect via Microsoft Teams / any configured channel)
2. Type a question related to your uploaded documents
3. SuperGinger retrieves relevant context and generates a precise, grounded answer

**Example Interactions:**

```
You:          Summarise the key points from the uploaded report.
SuperGinger:  The report highlights three main areas...

You:          What does the document say about data retention policies?
SuperGinger:  According to your document...

You:          Who are the key stakeholders mentioned?
SuperGinger:  The document references the following stakeholders...
```

---

## 📁 Project Structure

```
SuperGinger/
├── Super_Ginger/
│   ├── Controllers/                  # ASP.NET Core API controllers (bot endpoints)
│   ├── dialogs/                      # Bot Composer dialog definitions (conversation flows)
│   ├── knowledge-base/               # Your documents for AI-powered Q&A
│   ├── language-generation/          # LG templates for bot responses
│   ├── language-understanding/       # NLU / intent recognition configuration
│   ├── media/                        # Static media assets
│   ├── Properties/                   # .NET project properties
│   ├── recognizers/                  # Intent recognizer configurations
│   ├── schemas/                      # Bot schema definitions
│   ├── scripts/                      # Utility and setup scripts
│   ├── settings/                     # Bot and environment configuration files
│   ├── wwwroot/                      # Static web assets
│   ├── Program.cs                    # .NET application entry point
│   ├── Startup.cs                    # ASP.NET Core service configuration
│   ├── Super_Ginger.botproj          # Bot Composer project file
│   ├── Super_Ginger.csproj           # .NET project file
│   └── Nuget.config                  # NuGet package configuration
├── .deployment                       # Azure deployment configuration
├── .gitignore
└── README.md
```

---

## 🔒 Privacy & Security

SuperGinger is designed with privacy at its core:

- **No cloud API calls** — LLM inference happens entirely on your local machine via Ollama
- **No telemetry** — Your documents and conversations are never transmitted externally
- **Local knowledge base** — All documents are stored and queried locally within the `knowledge-base/` folder
- **You own your data** — Everything stays within your environment

This makes SuperGinger ideal for sensitive use cases such as legal documents, internal company policies, medical records, or personal research notes.

---

## 🤝 Contributing

Contributions are very welcome! Here's how to get involved:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature-name`)
3. Commit your changes (`git commit -m 'feat: add your feature'`)
4. Push to the branch (`git push origin feature/your-feature-name`)
5. Open a Pull Request

Please follow the existing code style and include relevant documentation for any new features.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE). See the `LICENSE` file for full details.

---

## 📬 Contact

**Atishay Jain** — [@atishayj281](https://github.com/atishayj281)

Project Link: [https://github.com/atishayj281/SuperGinger](https://github.com/atishayj281/SuperGinger)

---

*Built for privacy. Powered by open-source AI. 🫚*
