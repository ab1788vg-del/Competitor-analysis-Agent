# Competitor-analysis-Agent
This project is an end-to-end AI-powered Competitor Intelligence Agent that automatically collects competitor data, embeds it into a vector database, retrieves relevant information via RAG, and analyzes it using Google’s Gemini models. The system produces actionable competitive insights, strategic recommendations, and real-time alerts based on fresh web and news content.

📌 Features
✅ 1. Automated Web Scraping

The agent collects data from:

Competitor websites

Blog/Press/Updates pages

Google News articles

External mentions

It extracts clean text and builds a structured dataset of competitor information.

✅ 2. Embeddings + Vector Search (FAISS)

Uses Google’s text-embedding-004

Chunks documents into 250-word blocks

Creates embeddings for every chunk

Stores vectors in a FAISS L2 index

Enables fast, semantic retrieval of relevant content

✅ 3. Retrieval-Augmented Generation (RAG)

Queries are answered using a RAG pipeline:

Embeds the query

Retrieves top-k relevant chunks

Builds a structured prompt

Sends to Gemini 1.5 Flash / Pro for deeper reasoning

Output includes:

Summaries

Tactical implications

Priority & confidence

Source URLs

✅ 4. Real-Time Alerts

Detects competitor activities matching keywords:

Launch

Pricing

Acquired

Hiring

Beta

Announced

Alerts trigger when matched with recent content.

🏗 Architecture Overview
Web Scraper → Text Extractor → Chunker → 
Embedding Model → FAISS Index →
RAG Retriever → Gemini Analyst → Insights & Alerts

1. Collector

Fetches competitor pages and Google News results.
Handles:

HTML fetching

Duplicate avoidance

Basic error handling

2. Ingestor

Extracts clean text from HTML using BeautifulSoup, then stores:

URLs

Text

Timestamp

Source type

3. Chunking & Embedding

250-word chunks (40-word overlap)

Embeds with Google text-embedding-004

Saves FAISS index + chunk metadata

4. Retriever

Given a query:

Embeds it

Performs FAISS vector search

Returns closest matching chunks

5. Analyst

Uses Gemini to:

Summarize insights

Produce strategic recommendations

Provide evidence-linked outputs

6. Alerts Engine

Detects notable changes by scanning for predefined keywords and recent timestamps.

🚀 How to Run
1. Install Dependencies
pip install --upgrade pip
pip install requests beautifulsoup4 tqdm python-dotenv pandas
pip install faiss-cpu sentence-transformers
pip install google-generativeai

2. Enter Your Google API Key
import getpass, os
GOOGLE_API_KEY = getpass.getpass("Enter Google AI Studio API Key: ")
os.environ["GOOGLE_API_KEY"] = GOOGLE_API_KEY

3. Configure Generative AI Client
import google.generativeai as genai
genai.configure(api_key=os.environ["GOOGLE_API_KEY"])

4. Run the Notebook / Script Cells

Follow the cells in order:
1️⃣ Collector
2️⃣ Ingestor
3️⃣ Embeddings + FAISS
4️⃣ Retriever
5️⃣ Analyst
6️⃣ Alerts

Everything is modular and can run independently.

📊 Example Query
print(analyze("competitor.com", "product updates"))


Sample output:

3-sentence summary

3 strategic implications

Priority + confidence

Cited source URLs

📡 Alert Example
for kw, h in check_alerts("competitor.com"):
    print("ALERT:", kw, "→", h["url"])

🧠 Why This Project Matters

This agent solves a real business problem:
Companies struggle to track competitor movements manually. This system automates:

Data collection

Understanding

Analysis

Notifications

Powered by Google’s latest AI models and FAISS vector search, it delivers:

Accurate insights

Fast responses

Evidence-backed analysis

High extensibility

🔧 Customization

You can easily modify:

COMPANIES list

Keywords in the Alerts Engine

Retrieval depth (k)

Embedding model

LLM model (Flash / Pro)

Add more sources like:

Social media

Documentation pages

🛠 Technologies Used

Google Generative AI (Gemini family)

Google text-embedding-004

FAISS (Facebook AI Similarity Search)

BeautifulSoup4

Requests

Python

Pandas

TQDM

-----Future Improvements

Add support for RSS feeds

Integrate with Slack or email alerts

Build a dashboard UI

Add ORM + database layer

Continuous daily scraping scheduler

Multi-language support

⭐ Contributions & Feedback

Contributions are welcome!
Open an issue or submit a pull request to improve scraping, indexing, analysis, or alerting.

📜 License

This project is licensed under the MIT License.
