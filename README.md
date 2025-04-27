# RFQ-matching-using-n8n
📋 Overview
This project builds an automated n8n workflow that:

Accepts a Hebrew PDF of products via Telegram Bot,

Extracts the product descriptions,

Translates them using an LLM from OpenRouter,

Embeds both the translated descriptions and catalog descriptions into vectors,

Matches translated descriptions with catalog descriptions using cosine similarity,

Saves the matched results into a CSV,

Sends the CSV back to the user via Telegram Bot.

🔥 Workflow Steps (End-to-End)
Telegram Trigger

User uploads a Hebrew RFQ PDF through Telegram bot.

The workflow starts automatically.

Extract Text (Docling/Custom Extraction)

Parse the PDF.

Extract the second column ("תיאור" - description) which contains the product descriptions.

Translate Descriptions (OpenRouter LLM API)

Each extracted Hebrew description is translated into English.

This is done one-by-one using a LLM node via OpenRouter API.

Prepare Descriptions for Embedding

Catalog descriptions (already stored) and translated descriptions are merged together.

Data is structured as:

Column: description

Column: embedding

Embed Descriptions

Each description (both catalog and translated) is converted into vector embeddings.

Embeddings are either generated locally (custom server) or through another LLM.

Merge Inputs and Clean Up

Both catalog and translated embeddings are merged into a single input.

Proper parsing is ensured (arrays, not strings).

Matching Using Cosine Similarity

First 511 items are catalog embeddings.

Remaining items are translated embeddings.

For each translated description:

Compare against all catalog embeddings using cosine similarity.

Pick the best match if similarity exceeds a threshold (e.g., 0.85).

Generate Match Results

For every successful match:

Save the translated description and the matched catalog description.

Create CSV

Matched results are compiled into a CSV format (two columns):

translated_description

matched_catalog_description

CSV file is generated dynamically.

Send Back via Telegram

The CSV is converted into a binary file.

The bot sends the CSV file back to the user through the Telegram chat.

🛠️ Technical Stack
Framework: n8n

Language: JavaScript (for Function nodes)

LLM Provider: OpenRouter (Free models supported)

Vector DB: (Optional) Supabase or Local Server

Bot API: Telegram Bot API

Libraries Used: Buffer (for file conversion)

🧠 Special Handling
Waiting for Both Inputs: Before embedding or matching, catalog and translation data are synced carefully.

Error Handling:

Missing embeddings or parsing issues are skipped safely.

Clear error messages if input data is invalid.

Optimization:

Only relevant matches above similarity threshold are returned.

No unnecessary fields like embeddings are included in the final CSV.
