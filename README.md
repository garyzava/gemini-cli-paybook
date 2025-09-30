
# 🤖 Gemini CLI 101: A Practical Workflow Guide

Welcome! This repository is a beginner's guide to integrating Google's Gemini into your command-line interface (CLI) for a powerful, AI-driven development workflow. Think of it as having an AI pair programmer available right in your terminal.

This guide provides a reference for basic commands and showcases a complete, step-by-step example of how to build a web application from scratch using a structured, prompt-based process.

---

## 🚀 Getting Started: Installation

Pick one:

```bash
# Run instantly (no install)
npx https://github.com/google-gemini/gemini-cli

# Install globally with npm
npm install -g @google/gemini-cli

# Or with Homebrew (macOS/Linux)
brew install gemini-cli
```

Alternatevily, you will need a tool that allows you to access Gemini from your command line. The official way is often through the `gcloud` CLI or by using Google's SDKs. However, the community has built several user-friendly tools.

For this guide, we'll use `gemini` command for clarity. You can achieve the same results with tools like:
* **LLM by Simon Willison:** A powerful tool that supports Gemini and other models. ([Installation Guide](https://llm.datasette.io/en/stable/installation.html))
* **Google Cloud CLI:** The official way to interact with Google Cloud services, including AI Platform. ([Installation Guide](https://cloud.google.com/sdk/docs/install))

Once installed and configured with your API key, you can start using Gemini.

---

## ⌨️ Basic Commands Reference

Here are some common commands you'll find useful. The exact flags may vary depending on the tool you choose.

| Command                                                    | Description                                                                                                   |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `gemini "your prompt"`                                     | Sends a simple, direct prompt to Gemini.                                                                      |
| `gemini -f <file> "prompt about this file"`                | Sends a prompt along with the content of a file for context. Crucial for code-related tasks.                  |
| `gemini -f <file1> -f <file2> "prompt"`                    | Provides multiple files for broader context.                                                                  |
| `gemini "prompt" -o <output_file>`                         | Writes Gemini's response directly to a specified output file.                                                 |
| `gemini --multimodal <image.png> "prompt about image"`     | Uses Gemini's multimodal capabilities to analyze an image.                                                    |
| `gemini --chat`                                            | Starts an interactive chat session where the model remembers the conversation history.                       |
| `cat <file> | gemini "prompt about piped content"`        | Pipes the content of a file directly into Gemini. An alternative to the `-f` flag.                            |

---

## 📝 Example Workflow: Building a "Productivity Coach" App

This section walks you through a structured workflow to build a web app using Gemini. This method uses context files (`PRD.md`, `PLANNING.md`, etc.) to keep the AI aligned with your project goals.

### **Step 1: Create the Product Requirements Document (PRD)**

First, ask Gemini to generate a foundational PRD. This document will define the "what" and "why" of your project.

**→ Prompt:**
```bash
gemini -o PRD.md "Help me create a Product Requirements Document (PRD) for a web app that allows users to chat with a 'productivity coach'. The coach is based on 15 of the best books on productivity (I will provide my notes for these books). I want a clean, minimalist, and beautiful app."
````

### **Step 2: Create a `GEMINI.md` Meta-Instructions File**

This is the most important file. It tells Gemini *how* to behave during your development sessions.

**→ Prompt:**

```bash
gemini -f PRD.md -o GEMINI.md "Generate a GEMINI.md file from this PRD. This file will contain the core instructions to guide Gemini in all future coding sessions for this project."
```

Next, add your specific rules to this file. These rules ensure consistency in every interaction.

**→ Add to your `GEMINI.md` file:**

```markdown
Always read PLANNING.md at the start of every new conversation. Check TASKS.md before starting your work. Mark completed tasks in TASKS.md immediately, and add newly discovered tasks to TASKS.md when found.
```

### **Step 3: Create the `PLANNING.md` File**

Now, let's define the technical vision, architecture, and tech stack.

**→ Prompt:**

```bash
gemini -f PRD.md -o PLANNING.md "Create a PLANNING.md file that includes a vision statement, proposed architecture, recommended technology stack (e.g., frontend, backend, database), and a list of required tools for the app described in the PRD."
```

### **Step 4: Create the `TASKS.md` File**

Break down the project into actionable steps and milestones.

**→ Prompt:**

```bash
gemini -f PLANNING.md -o TASKS.md "Create a TASKS.md file with bullet-pointed tasks, divided into logical milestones, for building this app based on the planning document."
```

### **Step 5: Initiate the Build Process**

With all your planning documents in place, you can now ask Gemini to start coding. By providing all the context files, you ensure the AI has a complete understanding of the project.

**→ Prompt:**

```bash
gemini -f GEMINI.md -f PLANNING.md -f TASKS.md "Please read the attached files to understand the project. Then, complete the very first task listed in TASKS.md."
```

### **Step 6: Update Context and Summarize Progress**

Before ending a session or clearing your history, have Gemini summarize the work done. This keeps your `GEMINI.md` file updated with the latest project status.

**→ Prompt:**

```bash
gemini -f session_history.log "Please add a session summary to GEMINI.md summarizing what we’ve done so far. Use a '## Session Summaries' heading and add the new summary as a bullet point with today's date."
```

*(Note: `session_history.log` represents a log of your terminal commands and outputs from the current session.)*

-----

## 🔗 Useful Links

  * **Google AI for Developers:** Official source for Gemini API documentation and news. ([link](https://ai.google.dev/))
  * **The `gcloud` CLI Reference:** Official documentation for the Google Cloud CLI. ([link](https://cloud.google.com/sdk/gcloud/reference))
  * **Awesome Gemini:** A curated list of community projects and resources related to Gemini. ([link](https://www.google.com/search?q=https://github.com/dair-ai/awesome-gemini))
