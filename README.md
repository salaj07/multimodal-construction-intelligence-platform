# Multimodal Construction Intelligence Platform

Skill Wallet Capstone Project 1 — Streamlit application.

## Features
- **Site Safety & PPE Audit:** upload JPG/PNG photos, ask Gemini for a structured safety screening, review hazards, and download JSON.
- **Crack Diagnostics:** classify visible defects, communicate uncertainty about crack width, review next steps, and download JSON.
- **Planning & Valuation:** editable cost assumptions, indicative budget/CapEx/asset value, rough material quantities, progress and a Pollinations conceptual render link.
- **Daily Site Assistant:** weather-aware safety guidance and a multi-turn construction chatbot.

## Run locally
Python 3.9+ is the target; use a current supported Python version if possible.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
pip install -r requirements.txt
streamlit run app.py
```

Open the local URL shown by Streamlit.

## Gemini API
Enter your Google Gemini API key in the sidebar. The key is used for requests in the current Streamlit session and is not written to a database or file by this app. For deployment, prefer Streamlit secrets rather than sharing keys in screenshots or source control.

You can set a secret in `.streamlit/secrets.toml`:

```toml
GEMINI_API_KEY = "your-key"
```

The app currently uses a password input to avoid automatically loading secrets; paste the key into the sidebar. To change the model, edit the model field in the sidebar (default: `gemini-2.5-flash`).

Without a key, the safety and crack modules display clearly labelled demonstration output. Demo outputs are not derived from the uploaded image. The planning module works locally with editable assumptions.

## Deploy to Streamlit Community Cloud
1. Push `app.py`, `requirements.txt`, and `README.md` to a GitHub repository.
2. Create a new app in Streamlit Community Cloud and select `app.py`.
3. Add `GEMINI_API_KEY` under the app's Secrets settings if you later adapt the UI to load it automatically. As provided, paste it into the sidebar at runtime.
4. Deploy and test using non-sensitive sample images.

## Important limitations
- AI vision is an aid, not a certified PPE inspection or structural diagnosis.
- A photograph generally cannot verify hidden PPE such as steel-toe protection, nor provide reliable crack-width measurements without a visible scale.
- OSHA and Indian requirements vary by work, jurisdiction and project. IS 456 is a concrete code, not a PPE standard.
- Material quantities and valuation multipliers are illustrative planning assumptions, not a bill of quantities, QS estimate, or formal property appraisal. Validate against local rates, approved drawings, BOQ, and a qualified professional.
- The Pollinations link sends the prompt to an external service. Do not include confidential information.
- API calls require internet access and a valid Gemini API key. Errors fall back to demo outputs in the image-analysis tabs.
