# 🌐 Resume → Portfolio Website Generator

Upload a resume and get a clean, responsive personal website you can preview, customise and host for free.
Built with **Streamlit** and **Google Gemini Flash**.

## Features

- Upload a resume as **PDF, DOCX or TXT**
- Gemini extracts your details (name, skills, experience, projects, education, certifications, links)
- **Edit everything** before generating, and add or remove experience, project and education entries
- **4 themes** (Minimal Light, Dark Developer, Modern Gradient, Corporate Blue), **accent colour picker**, **3 font styles**
- Choose which sections to show; empty sections are skipped automatically
- Live preview, then **download a single self-contained `index.html`** (no external files, no JavaScript, no tracking)
- The website is responsive, uses semantic HTML, has keyboard focus styles, and picks readable text colours for any accent colour

## Run locally

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

streamlit run app.py
```

Get a free API key at <https://aistudio.google.com/apikey> and paste it into the sidebar.

### Optional: save the key so you don't paste it every time

Create `.streamlit/secrets.toml` (already in `.gitignore`, never commit it):

```toml
GEMINI_API_KEY = "your-key-here"
```

or set an environment variable: `export GEMINI_API_KEY=your-key-here`

### Choosing the Gemini model

The model id is editable in the sidebar (or set `GEMINI_MODEL`). Google renames and retires models from time to time, so check the current Flash id at <https://ai.google.dev/gemini-api/docs/models>. If the chosen model is not found, the app automatically tries the fallbacks listed in `FALLBACK_MODELS` at the top of `app.py`.

## Put the app on GitHub

```bash
git init
git add app.py README.md requirements.txt .gitignore
git commit -m "Initial commit: portfolio generator"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

Make sure `requirements.txt` (exact spelling, with an "s") is in the **root** of the repo next to `app.py`.

## Deploy the app on Streamlit Community Cloud

1. Go to <https://share.streamlit.io> and sign in with GitHub.
2. Click **Create app** → choose your repo, branch `main`, main file `app.py`.
3. (Optional) **Advanced settings → Secrets**, add `GEMINI_API_KEY = "your-key-here"`.
4. Click **Deploy**.

> ⚠️ If you add *your* key to Secrets, every visitor uses *your* quota. Leave it out and visitors can paste their own key in the sidebar.

**Seeing `ModuleNotFoundError`?** Streamlit didn't install your dependencies. Check that the file is named exactly `requirements.txt`, is in the repo root, and is pushed to GitHub. Then use **Manage app → Reboot app** and read the install log.

## Host the generated website for free

Click **Download index.html** in the app. Keep the file name `index.html`, then use any of these:

| Host | How |
|------|-----|
| **Netlify Drop** | Open <https://app.netlify.com/drop> and drag a folder containing `index.html` onto the page. You get a link instantly. |
| **GitHub Pages** | Create a repo, upload `index.html`, then **Settings → Pages → Deploy from a branch → main / (root)**. Live at `https://<username>.github.io/<repo>/`. Name the repo `<username>.github.io` for a clean address. |
| **Cloudflare Pages** | **Workers & Pages → Create → Pages → Upload assets**, upload the folder with `index.html`. |

Menu names on these sites change occasionally, but the idea is always the same: upload the file, get a link. A custom domain (e.g. `janedoe.com`) costs a few dollars per year at a registrar, and all three hosts support connecting one.

## Project structure

```
app.py             # UI, extraction, Gemini call, website builder
requirements.txt
README.md
.gitignore
```

## Limitations

- Scanned / image-only PDFs have no readable text, so the app asks for a text-based file instead.
- AI extraction can make mistakes. Always review the edit form before generating.
- Your resume text is sent to the Gemini API for extraction. Don't upload anything you aren't comfortable sending.
- The site uses system fonts (no web fonts) so it stays a single file that works offline.

## License

MIT# resume_to_portfolio_web_gen
