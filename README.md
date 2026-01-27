# Career Agent 🎯

A comprehensive AI-powered career development and job hunting toolkit designed for ML/AI professionals.

## Overview

Career Agent is a structured system of AI skills and resources to help with every stage of your job search journey - from finding the right opportunities to preparing for interviews and optimizing your application materials.

This project uses **Cursor AI** - an AI-powered code editor with specialized "Skills" (AI agents) that help automate job search tasks. Think of Skills as expert consultants you can call upon for specific tasks.

## Project Structure

```
career_agent/
├── .cursor/
│   └── skills/              # AI agent skills for Cursor
│       ├── job_agent/       # Job search and tracking
│       ├── cv_improvement/  # CV/resume optimization
│       ├── interview_prep/  # Interview preparation
│       └── [future skills]  # Additional career skills
├── data/                    # Job search data, applications tracking
├── scripts/                 # Automation scripts and utilities
├── prompts/                 # Reusable AI prompts and templates
└── README.md               # This file
```

## Getting Started

### Step 1: Install Cursor

1. **Download Cursor**
   - Visit [cursor.com](https://cursor.com/)
   - Download the installer for your operating system (Windows/Mac/Linux)
   - Free tier is available - no credit card required

2. **Install Cursor**
   - Run the installer
   - Follow the installation prompts
   - Cursor looks and works like VS Code (it's built on top of it)

3. **Launch Cursor**
   - Open the Cursor application
   - You'll see a familiar code editor interface

### Step 2: Open This Project

1. **Open the career_agent folder**
   - In Cursor: `File` → `Open Folder`
   - Navigate to and select the `career_agent` folder
   - Click "Open" or "Select Folder"

2. **Verify Skills are Loaded**
   - Cursor automatically detects skills in `.cursor/skills/` folders
   - Open the AI chat panel: Press `Cmd+L` (Mac) or `Ctrl+L` (Windows)
   - The chat panel appears on the right side

### Step 3: Test the Setup

Type this in the AI chat to verify everything is working:

```
What skills are available in this project?
```

You should see responses about: `job_agent`, `cv_improvement`, and `interview_prep`

## How to Use Skills

### Example: Finding Jobs with Job Agent

1. **Open AI chat:** Press `Cmd/Ctrl + L`

2. **Type your request:**
```
job agent, find me jobs
```

**Note:** 
- **First time in a chat:** Use `job agent, find me jobs` to help Cursor find the right skill
- **After that:** You can simply use `find me jobs` - Cursor maintains the context

3. **What to do next:**
   - Review the job details
   - If interested, manually add to `job_history.md`
   - If not interested, add company or specific job to `blacklist.md`

