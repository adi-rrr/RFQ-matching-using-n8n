**RFQ Product Matching System**

**📋 Overview**

This project automates the process of matching RFQ product descriptions with a master catalog using n8n, LLM translation, and vector similarity search.

**The system:**


Accepts a Hebrew PDF through Telegram,

Extracts product descriptions,

Translates them to English using an LLM,

Embeds both translated and catalog descriptions into vectors,

Matches them using cosine similarity,

Generates a CSV of matched results,

Sends the CSV file back via Telegram.

**🛠️ Tech Stack**

n8n (Automation Platform)

OpenRouter (LLM API for translation)

Local or external embedding server

Telegram Bot API

🎬 Full Walkthrough Video
➡️ Watch the full execution and explanation in : [https://drive.google.com/file/d/1VSacZTa9TE9GjvnruU3qylYcLsNCZG0e/view?usp=drive_link](url)

