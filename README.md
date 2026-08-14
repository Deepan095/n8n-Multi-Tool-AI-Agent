# 🤖 Multi-Tool AI Agent using n8n

A **multi-tool AI agent** built using **n8n, OpenAI, Telegram, Gmail, Google Calendar, Google Sheets, Google Docs, and SerpApi**.

The project demonstrates how a single AI Agent can understand natural-language instructions, decide which connected tool is required, execute the appropriate action, and return the result to the user through Telegram.

This project was developed as part of my hands-on learning in **Generative AI, AI Agents, tool calling, API automation, and workflow automation using n8n**.

---

## 📌 Project Overview

A normal chatbot mainly generates text responses.

This project goes one step further by giving an **AI Agent access to multiple tools**.

Instead of manually selecting a workflow, the user can simply send a natural-language instruction through Telegram.

For example:

```text
Send an email to John.
```

or:

```text
Create a calendar event tomorrow at 10 AM.
```

or:

```text
Search Google for Generative AI applications.
```

The AI Agent understands the request and selects the appropriate tool.

---

## 🏗️ Workflow Architecture

```text
                        Telegram User
                              │
                              ▼
                       Telegram Trigger
                              │
                              ▼
                         ┌─────────┐
                         │AI Agent │
                         └────┬────┘
                              │
              ┌───────────────┼────────────────────┐
              │               │                    │
              ▼               ▼                    ▼
        OpenAI Model      Simple Memory          Tools
                                                   │
                         ┌─────────────────────────┼───────────────┐
                         │          │              │               │
                         ▼          ▼              ▼               ▼
                       Gmail    Calendar      Google Sheets    Google Docs
                                                                    │
                                                                    ▼
                                                              Google Search
                                                               (SerpApi)

                              │
                              ▼
                    Telegram Send Message
                              │
                              ▼
                            User
```

---

# ⚙️ How It Works

## 1. Telegram Trigger

Telegram acts as the user interface for the AI Agent.

When a user sends a message to the Telegram bot, the workflow starts automatically.

Example:

```text
Create a meeting tomorrow at 11 AM.
```

The message is passed to the AI Agent.

---

## 2. AI Agent

The AI Agent is the main decision-making component of the workflow.

It receives the user's natural-language request and determines what action needs to be performed.

The agent can decide:

```text
Need to send email?
        ↓
Use Gmail

Need to create meeting?
        ↓
Use Google Calendar

Need to update spreadsheet?
        ↓
Use Google Sheets

Need to create a document?
        ↓
Use Google Docs

Need information from the web?
        ↓
Use Google Search
```

This demonstrates **AI Agent tool selection and tool calling**.

---

## 3. OpenAI Chat Model

The OpenAI Chat Model provides the language understanding and reasoning capability for the AI Agent.

It helps the agent understand what the user wants and determine which available tool should be used.

```text
User Instruction
       ↓
OpenAI Chat Model
       ↓
Understand Intent
       ↓
AI Agent
       ↓
Select Tool
```

---

## 4. Simple Memory

The workflow includes conversational memory.

Memory allows the AI Agent to retain recent conversational context instead of treating every Telegram message as completely unrelated.

For example:

```text
User:
Search for Generative AI applications.

User:
Now create a document about it.
```

Memory helps the agent understand that the second instruction relates to the previous conversation.

---

# 🧰 Tools Available to the AI Agent

## 📧 Gmail — Send Mail

The Gmail tool allows the AI Agent to send emails based on user instructions.

Example:

```text
Send an email to example@email.com saying
the meeting has been confirmed.
```

---

## 📅 Google Calendar — Create Event

The Google Calendar tool allows the AI Agent to create calendar events.

Example:

```text
Create a meeting tomorrow at 3 PM.
```

The agent identifies that this requires the Calendar tool and creates the event using the configured Google Calendar account.

---

## 📊 Google Sheets — Update Content

The Google Sheets tool allows the AI Agent to append or update information in a spreadsheet.

Example:

```text
Add this information to my Google Sheet.
```

---

## 📄 Google Docs — Create Document

The Google Docs tool allows the AI Agent to create new documents.

Example:

```text
Create a Google Doc about Generative AI applications.
```

---

## ✏️ Google Docs — Update Document

The AI Agent can also update content inside a Google document.

This makes multi-step workflows possible.

For example:

```text
Search for Generative AI applications
and create a document containing the information.
```

The workflow can involve:

```text
User
 ↓
AI Agent
 ↓
Google Search
 ↓
Get Information
 ↓
Create Google Doc
 ↓
Update Document
 ↓
Return Result
```

---

## 🔎 Google Search — SerpApi

The workflow uses SerpApi as a search tool.

The AI Agent can use it when external information is required.

Example:

```text
Search Google for applications of Generative AI.
```

Instead of relying only on the LLM's existing knowledge, the agent can call the search tool.

---

# 🧠 What Makes This a Multi-Tool Agent?

A traditional workflow usually follows a predefined path:

```text
Input
 ↓
Step 1
 ↓
Step 2
 ↓
Step 3
```

This project is different.

The AI Agent has access to several tools and determines which one is appropriate for the user's request.

```text
                   AI Agent
                      │
        ┌─────────────┼─────────────┐
        │             │             │
      Gmail       Calendar        Search
        │             │             │
        └─────────────┼─────────────┘
                      │
                   Google
                Docs / Sheets
```

The agent does not need to use every tool for every request.

It selects tools based on the task.

---

# 🔄 Example Multi-Step Task

A more advanced instruction could be:

```text
Search about Generative AI applications,
create a Google document,
and add the researched information to it.
```

Conceptually, the agent performs:

```text
Telegram
   ↓
AI Agent
   ↓
Understand Request
   ↓
Google Search
   ↓
Collect Information
   ↓
Create Google Doc
   ↓
Update Google Doc
   ↓
Generate Final Response
   ↓
Telegram
```

This demonstrates how an AI Agent can coordinate **multiple tools to complete one user goal**.

---

# 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and AI orchestration |
| OpenAI | Language model for the AI Agent |
| Telegram | User interface |
| Gmail | Sending emails |
| Google Calendar | Creating calendar events |
| Google Sheets | Updating spreadsheet data |
| Google Docs | Creating and updating documents |
| SerpApi | Google search |
| Simple Memory | Maintaining conversation context |

---

# 📸 Workflow

The workflow consists of a Telegram-based AI Agent connected to multiple tools.

```text
Telegram Trigger
       ↓
    AI Agent
       ↓
Telegram Response
```

The AI Agent has access to:

```text
OpenAI Chat Model
Simple Memory
Gmail
Google Calendar
Google Sheets
Google Docs - Create
Google Docs - Update
Google Search - SerpApi
```

### Workflow Screenshot

![Multi Tool AI Agent Workflow](screenshots/multi-tool-ai-agent.png)

---

# 💬 Example Commands

### Email

```text
Send an email to example@email.com saying
the project has been completed.
```

### Calendar

```text
Create a meeting tomorrow at 11 AM.
```

### Google Search

```text
Search Google for the latest applications of Generative AI.
```

### Google Docs

```text
Create a document called GenAI Applications.
```

### Google Sheets

```text
Add this information to my spreadsheet.
```

### Multi-Step Task

```text
Search about Generative AI applications,
create a document and add the information to it.
```

---

# 📂 Repository Structure

```text
n8n-Multi-Tool-AI-Agent/
│
├── README.md
│
├── workflow/
│   └── multi-tool-ai-agent.json
│
└── screenshots/
    └── multi-tool-ai-agent.png
```

---

# 🚀 How to Import the Workflow

1. Download the workflow JSON file.
2. Open n8n.
3. Import the workflow.
4. Configure your own credentials.
5. Configure your Telegram bot.
6. Configure the required Google integrations.
7. Configure OpenAI.
8. Configure SerpApi.
9. Test each tool individually.
10. Test the complete AI Agent workflow.
11. Activate/publish the workflow when everything works correctly.

---

# 🔑 Required Integrations

To run the complete workflow, users need to configure their own credentials for:

- Telegram
- OpenAI
- Gmail / Google
- Google Calendar
- Google Sheets
- Google Docs
- SerpApi

Credentials are **not included in this repository**.

---

# 🔐 Security

Sensitive credentials and instance-specific information should be removed from the exported workflow before publishing it to GitHub.

The public workflow should not contain:

```text
API keys
Telegram bot tokens
OAuth tokens
Passwords
Credential references
Webhook IDs
n8n instance IDs
Private environment variables
```

Users importing this project must configure their own credentials.

---

# 🎯 Concepts Demonstrated

This project demonstrates:

- Generative AI
- Large Language Models (LLMs)
- AI Agents
- Multi-Tool AI Agents
- Tool Calling
- Agentic Workflows
- Prompt Engineering
- Conversational Memory
- API Automation
- Workflow Automation
- Google Workspace Automation
- Telegram Bot Integration
- Search Integration
- Low-Code AI Development
- Multi-Step AI Tasks
- AI Orchestration with n8n

---

# 🎓 Learning Outcomes

Through this project, I practiced:

- Creating an AI Agent in n8n
- Connecting an OpenAI model to an agent
- Giving an AI Agent multiple tools
- Allowing the agent to choose tools dynamically
- Connecting Telegram to an AI workflow
- Sending emails through an AI Agent
- Creating Google Calendar events
- Updating Google Sheets
- Creating Google Docs
- Updating Google Docs
- Performing Google searches using SerpApi
- Using conversational memory
- Passing data between tools
- Building multi-step agent workflows
- Handling credentials securely
- Exporting n8n workflows for GitHub

---

# 🔮 Future Improvements

Possible improvements include:

- Human-in-the-loop approval before sending emails
- Approval before creating calendar events
- More persistent memory
- Database integration
- RAG integration
- Multiple specialized AI agents
- MCP integrations
- Error handling and retry mechanisms
- Structured logging
- User authentication
- Better tool permission controls

These improvements could evolve the project from a simple multi-tool agent into a more advanced **agentic automation system**.

---

# ⚠️ Disclaimer

This project was created for educational and portfolio purposes.

Users should review and configure tool permissions carefully before allowing an AI Agent to perform actions such as sending emails, modifying documents, updating spreadsheets, or creating calendar events.

---

## 👨‍💻 Author

**Deepan**

Generative AI & Automation Learner

Hands-on learning with:

`n8n` • `Generative AI` • `AI Agents` • `LLMs` • `Tool Calling` • `APIs` • `Automation`
