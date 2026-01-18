# AI-Research-Agent
# The AI Research Agent: An Autonomous Intelligence Analyst

This isn't just a workflow; it's a complete, autonomous system for strategic career intelligence. Built with n8n, this agent automatically monitors the web for relevant job openings and tech news, scrapes the content, and uses the Google Gemini AI to deliver a concise, actionable intelligence briefing every morning.


---

## The Mission: Turning Noise into Signal

In today's fast-paced job market, staying informed is a full-time job. Manually tracking dozens of companies, news sites, and job boards is time-consuming and inefficient.

The AI Research Agent solves this problem. It acts as a personal intelligence analyst that works for you 24/7, even while you sleep. Its mission is to transform the overwhelming noise of the internet into a clear, strategic signal, ensuring you never miss a critical opportunity.

## Core Architecture & Features

The agent is built as a multi-stage n8n workflow, with each node representing a distinct phase of the intelligence cycle.

1.  **The Trigger (Schedule Node):** The workflow is fully autonomous, initiating automatically every morning at a scheduled time.

2.  **The Search (Code + Serper API):** The agent begins by performing a series of automated Google searches for a customizable list of key phrases (e.g., "entry-level software jobs in Lagos," "Paystack hiring," "Andela new projects").

3.  **The Filtering & Validation (Code Node):** Raw search results are messy. This stage uses custom code to filter for the most relevant links and validate them, discarding any invalid or unscrapable URLs (like direct LinkedIn links) to ensure data quality.

4.  **The Scraping (Loop + Wait + ScrapingBee API):** The core data acquisition module. It patiently processes each validated URL one by one, using a rate-limiting loop to respectfully manage API calls. It leverages the powerful ScrapingBee API to retrieve the full text content from each page.

5.  **The Synthesis (Google Gemini Node):** This is the AI "brain." The aggregated text from all scraped sources is fed to the Gemini AI with a sophisticated "Intelligence Analyst" prompt, instructing it to summarize key findings, identify opportunities, and generate a clean report.

6.  **The Delivery (Email/Messaging Node - *To be activated*):** The final, AI-generated briefing is sent directly to the user via their preferred channel.

## A Story of Real-World Engineering: Overcoming Challenges

This project was built to be resilient and to conquer the common challenges of real-world automation.

#### Challenge 1: Taming the Flood (Rate Limiting)
*   **Problem:** Initial tests sent dozens of API requests simultaneously, triggering `429 - Too Many Requests` errors from the server.
*   **Solution:** A `Loop Over Items -> Wait` structure was architected. This forces the workflow to process only one URL at a time, with a programmable pause between each request, ensuring the agent is both effective and respectful of API limits.

#### Challenge 2: The Fortress (Advanced Anti-Bot Protection)
*   **Problem:** Many target sites (like Indeed.com) are protected by sophisticated anti-bot services like Cloudflare, which blocked initial scraping attempts.
*   **Solution:** The system was upgraded to use the ScrapingBee API with the `premium_proxy` parameter enabled. Furthermore, the HTTP Request node was configured with `Continue On Fail` and followed by a "Quality Control" `Code` node. This allows the agent to bypass most security measures and intelligently discard any results from the few pages it still cannot access, preventing the entire workflow from crashing.

## Technology Stack

*   **Automation Platform:** [n8n.io](https://n8n.io/) (Self-Hosted)
*   **AI Model:** [Google Gemini 1.5 Flash](https://deepmind.google/technologies/gemini/)
*   **Search API:** [Serper.dev](https://serper.dev/)
*   **Web Scraping API:** [ScrapingBee.com](https://www.scrapingbee.com/)

## Current Status: Demonstration Mode

**The scraping module of this agent is so effective that it successfully exhausted its monthly free API credit limit during final testing.** This is a testament to the system's robustness and ability to run at scale.

For demonstration purposes on this repository, the live scraping loop has been temporarily deactivated. In its place, a `Code` node containing high-quality mock data has been injected. This allows the most critical part of the workflow—the AI Synthesis—to be demonstrated fully.

The complete, autonomous workflow can be reactivated simply by enabling the scraping nodes and ensuring the necessary API keys have available credits.

---

This agent is the third pillar in a **Professional AI Suite**, joining its sibling projects:
*   **The Hunter:** A high-volume, personalized outreach tool.
*   **The Farmer:** An AI-powered ghostwriter for building a personal brand.
