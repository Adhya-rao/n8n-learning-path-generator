# 🤖 AI Learning Path Generator Agent

## 📌 Overview
The **AI Learning Path Generator** is an intelligent automation system that creates a **structured learning plan** based on a user's learning goal.

Instead of manually planning courses and searching for resources, this AI agent automatically:

- Understands your learning goal
- Creates a **day-wise curriculum**
- Researches relevant learning resources
- Generates a **Google Document with the learning plan**
- Schedules learning sessions in **Google Calendar**

The system is built using **n8n workflow automation**, **Google Gemini AI**, and external tools like **SerpAPI**, **Google Docs**, and **Google Calendar**.

---

# 🚀 What This Project Does

When a user sends a learning goal such as:

```
Create a 5-day learning plan for React starting tomorrow
```

The AI agent will automatically:

1. Plan a **day-wise curriculum**
2. Search the web for **learning resources**
3. Generate a **Google Document with the learning plan**
4. Create **calendar events for each learning session**

---

# ⚙️ Workflow Architecture

```
Chat Trigger
     ↓
AI Agent
     ↓
Google Gemini Chat Model
     ↓
SerpAPI (Research Resources)
     ↓
Google Docs (Create Document)
     ↓
Google Docs (Update Document)
     ↓
Google Calendar (Schedule Events)
```

---

# 🧰 Technologies Used

- **n8n** – Workflow automation
- **Google Gemini AI (gemini-2.0-flash)** – AI reasoning and planning
- **SerpAPI** – Web research and resource discovery
- **Google Docs API** – Create and update learning plan document
- **Google Calendar API** – Schedule learning sessions
- **Google Cloud OAuth** – Authentication for Google services

---

# 📋 Prerequisites

Before building this workflow you need:

- n8n account
- Google account
- Google Cloud project
- SerpAPI account
- Google API credentials

Required APIs:

- Google Docs API
- Google Drive API
- Google Calendar API

---

# ⚙️ Workflow Steps

---

# 1️⃣ Chat Trigger

The **Chat Trigger Node** provides a chat interface for the user.

It activates the workflow when the user sends a message.

Example input:

```
Create a 7 day learning plan for Python starting tomorrow
```

### Configuration

- Place **Chat Trigger** at the start of the workflow
- Connect it to the **AI Agent**

---

# 2️⃣ AI Agent Setup

The **AI Agent Node** acts as the brain of the system.

It:

- Understands the learning goal
- Plans the curriculum
- Uses tools to complete tasks

### Configuration

- Add **AI Agent Node**
- Connect to **Chat Trigger**
- Add **Google Gemini Chat Model**

### Model Used

```
gemini-2.0-flash
```

Provide an API key from **Google AI Studio**.

---

# 3️⃣ Research Resources using SerpAPI

SerpAPI allows the agent to search the internet for learning resources.

### What SerpAPI Can Do

- Find **YouTube tutorials**
- Discover **articles and blogs**
- Retrieve **learning documentation**
- Provide **resource URLs**

---

# ⚠️ Known Issue

Currently the **SerpAPI Tool Node in n8n has open issues** and may fail.

### Workaround

Use an **HTTP Request Node** instead.

---

# 🔧 Integrating SerpAPI using HTTP Request

Steps:

1. Add **HTTP Request Node**
2. Connect it as a tool to the **AI Agent**
3. Import the **cURL request from SerpAPI**
4. Configure request parameters

This allows the agent to perform web research successfully.

---

# 4️⃣ Creating Google Docs

The workflow generates a **Google Document** that stores the learning path.

### What the Tool Does

- Creates a new document
- Assigns a title
- Returns the document ID

Example title:

```
5-Day React Learning Path
```

---

# 🔐 Google Docs API Setup

Before adding the node you must configure **Google Cloud OAuth**.

Steps:

1. Create a **Google Cloud Project**
2. Enable APIs:
   - Google Docs API
   - Google Drive API
3. Configure **OAuth Consent Screen**
4. Create **OAuth Client ID**
5. Copy **Client ID and Client Secret**
6. Add them inside **n8n credentials**

---

# 5️⃣ Updating the Document

After creating the document, the agent fills it with the learning plan.

### What the Tool Does

- Inserts **daily topics**
- Adds **learning objectives**
- Includes **resource links**
- Formats the learning schedule

Configuration:

- Add **Google Docs Tool Node**
- Select **Update Document**
- Use the same OAuth credentials

---

# 6️⃣ Scheduling Calendar Events

To help users stay committed to learning, the agent schedules sessions in **Google Calendar**.

### What the Tool Does

- Creates an event for each day
- Schedules consecutive dates
- Allocates **2-hour learning blocks**
- Includes learning content in the event description

Example event:

```
Day 1 – React Fundamentals
Duration: 2 Hours
Resources:
- React Documentation
- YouTube Tutorial
- Blog Articles
```

---

# 🔐 Google Calendar API Setup

Ensure the **Google Calendar API** is enabled in your Google Cloud project.

Configuration:

- Add **Google Calendar Tool Node**
- Select **Create Event**
- Connect OAuth credentials

The AI agent will call this tool **multiple times** (once per learning day).

---

# 🧠 AI Agent System Instructions

Add the following prompt in the **System Message** field of the AI Agent.

```
Never leave Summary or Description empty
Calculate start date from user input or use today

You are a day-wise learning path generator.

When given a learning goal, create a curriculum with Google Docs and Calendar events.

STEP 1: PLAN THE CURRICULUM
Plan topics based on the number of days requested.
Structure topics from beginner to advanced.

STEP 2: DETERMINE START DATE
If user says "starting tomorrow" → use tomorrow
If user says "starting next Monday" → calculate next Monday
If user says "starting from [date]" → use that date
If no date mentioned → use today's date

Today is {{$now.format('YYYY-MM-DD')}}
```

---

# 🧪 Example User Request

```
Create a 5 day learning plan for React starting tomorrow
```

---

# 📄 Output Generated

The AI agent will produce:

1️⃣ **Google Document**

- Day-wise curriculum
- Learning topics
- Resource links

2️⃣ **Google Calendar Events**

- One event per learning day
- 2-hour learning session
- Resource links included

---

# 🔄 Final Workflow

```
Chat Trigger
      ↓
AI Agent
      ↓
Google Gemini Chat Model
      ↓
SerpAPI Research (HTTP Request)
      ↓
Google Docs Create Document
      ↓
Google Docs Update Document
      ↓
Google Calendar Create Event
```

---

# 🎯 Key Benefits

✔ Automated learning path generation  
✔ AI-powered curriculum planning  
✔ Integrated research using SerpAPI  
✔ Automatic document creation  
✔ Calendar scheduling for consistency  

---

# 🚀 Future Improvements

- Personalized difficulty levels
- Weekly learning summaries
- Progress tracking dashboard
- Integration with Notion
- Slack or Email reminders
- Multi-topic learning paths

---

# 🏆 Result

With this automation you now have a **fully autonomous AI learning assistant** that can transform a simple request into a **structured learning plan with resources and scheduled sessions.**
