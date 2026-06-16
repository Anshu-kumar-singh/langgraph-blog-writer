# LangGraph Blog Writer

An AI-powered multi-agent blog generation system built with **LangGraph**, **LangChain**, and **Streamlit**.

This project automatically generates structured, research-backed blog posts using a graph-based orchestration workflow. It can:

* Plan blog structure
* Perform web research when needed
* Generate section-wise content using worker agents
* Merge all generated sections
* Decide where images are needed
* Generate AI image prompts and placeholders
* Export blogs with images

---

# Features

## Multi-Agent Blog Generation

The system uses a graph-based architecture where different nodes handle specialized tasks such as:

* Routing
* Research
* Planning
* Writing
* Reducing/Merging
* Image generation

---

## Intelligent Research Routing

Before generating content, the system determines whether external research is needed.

Supported modes:

* **Closed Book** → Uses only model knowledge
* **Hybrid** → Uses model knowledge + research
* **Open Book** → Heavy research-based generation

---

## Structured Blog Planning

The orchestrator creates a detailed blog plan including:

* Blog title
* Audience
* Tone
* Blog type
* Writing constraints
* Section breakdown
* Word targets
* Research requirements

---

## Parallel Content Generation

Each blog section is generated independently using worker nodes.

This allows:

* Faster generation
* Better modularity
* Easier scaling
* Cleaner section-focused writing

---

## AI Image Planning

The system can automatically:

* Detect where visuals are useful
* Create image placeholders
* Generate image prompts
* Insert captions and alt text

Example:

```markdown
[[IMAGE_1]]
```

---

## Streamlit Frontend

A clean Streamlit UI allows users to:

* Enter a blog topic
* Generate blogs interactively
* Stream graph progress
* Preview generated markdown
* Download blog ZIP packages
* Export generated images

---

# Architecture Overview

```text
User Input
    │
    ▼
Router Node
    │
    ├── Research Needed?
    │         │
    │         ▼
    │     Research Node
    │
    ▼
Orchestrator Node
    │
    ▼
Worker Nodes (Parallel Section Writers)
    │
    ▼
Reducer Node
    │
    ▼
Image Decision Node
    │
    ▼
Image Generation Node
    │
    ▼
Final Blog Output
```

---

# Project Structure

```text
Blog_writing_agent/
│
├── bwa_backend.py        # LangGraph workflow and agent logic
├── bwa_frontend.py       # Streamlit UI
├── requirements.txt      # Dependencies
```

---

# Core Components

## 1. Router

Determines:

* Whether research is required
* Research mode
* Search queries
* Depth of information gathering

---

## 2. Research Node

Collects evidence and sources using external search tools.

Stores:

* URLs
* Snippets
* Titles
* Publication dates

---

## 3. Orchestrator

Creates the full blog execution plan.

Defines:

* Tasks
* Goals
* Bullet points
* Word counts
* Writing requirements

---

## 4. Worker Nodes

Generate individual sections of the blog independently.

Each worker receives:

* Section objective
* Context
* Research evidence
* Writing constraints

---

## 5. Reducer

Combines all generated sections into a single coherent markdown document.

Handles:

* Formatting
* Section ordering
* Consistency
* Final cleanup

---

## 6. Image Pipeline

The image pipeline works in 3 stages:

### merge_content

Combines generated markdown sections.

### decide_images

Determines where visuals improve understanding.

### generate_and_place_images

Creates image specifications including:

* Prompt
* Filename
* Caption
* Alt text
* Resolution

---

# Technologies Used

## Backend

* LangGraph
* LangChain
* OpenAI
* Pydantic
* Python

## Frontend

* Streamlit

## Research

* Tavily Search API

## Image Generation

* Google Gemini API

---

# Installation

## Clone the Repository

```bash
git clone <repo-url>
cd Blog_writing_agent
```

---

## Create Virtual Environment

```bash
python -m venv venv
```

Activate:

### Windows

```bash
venv\Scripts\activate
```

### Linux / Mac

```bash
source venv/bin/activate
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Environment Variables

Create a `.env` file:

```env
OPENAI_API_KEY=your_openai_key
TAVILY_API_KEY=your_tavily_key
GOOGLE_API_KEY=your_google_key
```

---

# Running the Application

## Start Streamlit

```bash
streamlit run bwa_frontend.py
```

---

# Example Workflow

1. User enters a topic
2. Router checks research requirements
3. Research node gathers evidence
4. Orchestrator creates blog plan
5. Workers generate sections
6. Reducer merges content
7. Image planner inserts visual placeholders
8. Final markdown and assets are exported

---

# Output

The system generates:

* Markdown blog file
* Generated image assets
* ZIP package for download

---

# Example Use Cases

* Technical blogs
* AI tutorials
* Product explainers
* System design articles
* News roundups
* Educational content

---

# Future Improvements

Potential enhancements:

* Citation formatting
* SEO optimization
* Multi-language support
* Real image generation APIs
* Vector database memory
* Human-in-the-loop editing
* Publishing integrations

---

# Why LangGraph?

LangGraph enables:

* Stateful workflows
* Multi-agent orchestration
* Parallel execution
* Reliable branching logic
* Scalable AI pipelines

This makes it ideal for long-form autonomous content generation systems.

---

# License

MIT License

---

# Acknowledgements

Built using:

* LangGraph
* LangChain
* OpenAI
* Streamlit
* Tavily
* Google Gemini
