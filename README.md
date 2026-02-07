# Sales Brochure Generator

Generate a company brochure in markdown by scraping a website and using an LLM to pick relevant pages (About, Careers, etc.) and summarize them.

## How it works

1. **Scrape** – Fetches the landing page and all links from the given URL.
2. **Select** – An LLM (Gemini) chooses links that are useful for a brochure (e.g. About, Careers, company info), ignoring Terms, Privacy, etc.
3. **Gather** – Fetches the text content of the landing page and each selected link (capped at 2,000 characters per page).
4. **Generate** – The LLM writes a short markdown brochure for customers, investors, and recruits.

You can get the brochure in one shot or stream it in the notebook.

## Project structure

```
Sales_Brochure_Generator/
├── brochure.ipynb    # Main notebook: setup, link selection, brochure generation
├── scraper.py        # fetch_website_links(url), fetch_website_contents(url)
├── requirements.txt
├── .env              # GEMINI_API_KEY (not committed)
└── README.md
```

## Setup

1. **Clone and enter the project**
   ```bash
   cd Sales_Brochure_Generator
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv .venv
   .venv\Scripts\activate   # Windows
   # source .venv/bin/activate   # macOS/Linux
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure API key**
   - Copy `.env.example` to `.env` (or create `.env`).
   - Add your Gemini API key:
     ```
     GEMINI_API_KEY=your_key_here
     ```
   - Get a key: [Google AI Studio](https://aistudio.google.com/apikey).

## Usage

1. Open **`brochure.ipynb`** in Jupyter or VS Code.
2. Run the cells from top to bottom (imports, `load_dotenv`, Gemini client, prompts, and helper functions).
3. Generate a brochure:
   - **One-shot:**  
     `create_brochure("CompanyName", "https://example.com")`
   - **Streaming:**  
     `stream_brochure("CompanyName", "https://example.com")`

Example:

```python
create_brochure("Hugging Face", "https://huggingface.co")
# or
stream_brochure("Hugging Face", "https://huggingface.co")
```

## Requirements

- Python 3.8+
- **Gemini API key** (used via OpenAI-compatible API in the notebook)

| Package         | Purpose                    |
|----------------|----------------------------|
| requests       | HTTP requests for scraping |
| beautifulsoup4 | Parse HTML                  |
| python-dotenv  | Load `.env`                 |
| openai         | OpenAI client (Gemini endpoint) |
| ipython        | Run notebook, `display`/Markdown |

## Optional: local LLM (Ollama)

The notebook includes commented code to use Ollama instead of Gemini. Uncomment the Ollama cell and set `llm_call = ollama` to use a local model.
