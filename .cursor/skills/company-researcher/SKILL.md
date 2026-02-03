---
name: company-researcher
description: Research and summarize company information for job applications. Use when the user asks to check a company, analyze a potential employer, or after job listings are provided.
---

# Company Researcher

## Overview
This skill researches companies to help the user make informed decisions about job applications. It focuses on stability, culture, and recent news.

## Information to Gather
For each company, use `web_search` to find:

1.  **Core Business**: What do they do? (Industry, Product/Service)
2.  **Scale**: Number of employees, HQ location.
3.  **Financial Health**:
    *   Public/Private?
    *   Funding stage (if private, e.g., Series A, B, C).
    *   Stock performance (if public, 1-year trend summary).
4.  **Recent News (Last 6-12 months)**:
    *   **Layoffs**: Explicitly search for "[Company Name] layoffs".
    *   Acquisitions or Mergers.
    *   Major product launches or strategic shifts.
5.  **Culture & Reputation**:
    *   Glassdoor/Blind sentiment (if available in search snippets).
    *   Remote work policy (if mentioned).
6.  **Commute Analysis**:
    *   Read `career_agent/.cursor/skills/company-researcher/private/user_context.md` to get the user's home address.
    *   Use `web_search` to find the commute time from the home address to the company's HQ or relevant office location (e.g. "commute from [Home Address] to [Company Office] by car" and "by public transport").
    *   Note: Do **NOT** reveal the specific home address in the final output. Use generic terms like "Home".

## Output Format
Provide a summary for each company:

### [Company Name]
*   **Industry:** [Industry]
*   **Size:** [Number of employees]
*   **Status:** [Public/Private - Funding Stage]
*   **Commute (from Home):**
    *   🚗 **Car:** [Time]
    *   🚆 **Public Transit:** [Time]
*   **Key Findings:**
    *   [News item]
    *   [Culture point]
*   **Red Flags:** 🚩 [Any layoffs, lawsuits, or negative press] (or "None detected")
*   **Sources:** [Links to sources]

## Usage Tips
*   If checking multiple companies, process them in parallel if possible, or sequentially if the list is long.
*   Prioritize "Red Flags" like recent layoffs as this is critical for job security.
