# DevLog — AI Daily Update Generator

> Turn your GitHub/GitLab commits into a polished daily status report in one click.

DevLog connects to your repositories, reads your commits for the day, and uses **Google Gemini AI** to generate a clean, professional daily update — formatted as a summary + task table, ready to paste into Outlook, email, or any report.

🔗 **Live Demo → [[https://daily-update-generator.netlify.app/](https://daily-update-generator.netlify.app/)]**

---

## ✨ Features

### 🔗 Git Integration
- Fetch commits by date from **GitHub** and **GitLab**
- Support for **multiple repos and branches** in a single report
- Token-based auth — your credentials never leave your browser or touch the server

### 🤖 AI-Generated Reports
Powered by **Google Gemini**, DevLog automatically:
- Writes a professional 2–3 sentence daily summary
- Produces a structured task table with project, description, hours, status, and remarks
- Caps and proportionally distributes hours (max 8h/day)

### 📧 Share-Ready Output
- **Copy Full Report** — HTML email optimized for Outlook and Word
- **Copy Table** — HTML + TSV for pasting into docs or spreadsheets
- **Send via Email** — Outlook Desktop, Office 365, Outlook.com, Gmail, or `.eml` download
- **Print / Export PDF**

### 🎨 Developer-First UX
- Dark, modern UI built for developer workflows
- Commit preview panel with grouped results by repo/branch
- Searchable multi-select dropdowns for repos and branches
- Editable hours per task with live budget bar
- Remembers your project name, dev name, and GitHub config locally

---

## 🛡️ Security & Privacy

DevLog is designed to be **safe to open source** — no secrets ever touch the repo.

| What | Where it lives | Committed? |
|---|---|---|
| `GOOGLE_API_KEY` | `.env` file / hosting env vars | ❌ Never |
| GitHub / GitLab tokens | Browser only (client-side API calls) | ❌ Never |
| User config (name, project) | `localStorage` in the browser | ❌ Never |

- API keys are loaded **only** from environment variables
- `.env` is in `.gitignore` — keys are never committed
- GitHub/GitLab tokens are used only for direct API calls from your machine and are **not stored or logged** on the backend

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Single `index.html` — Vanilla JS + CSS, no build step |
| Backend | `server.js` — Node.js + Express |
| AI | Google Gemini via `@google/generative-ai` |
| Deployment | Vercel (backend) + Netlify or any static host (frontend) |

---

## 🚀 Getting Started (Local)

### 1. Clone the repo

```bash
git clone https://github.com/pankajmadhikar/generative-ai-learning.git
cd generative-ai-learning
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create your `.env` file

```bash
cp .env.example .env
```

Then edit `.env`:

```env
GOOGLE_API_KEY=your_gemini_api_key_here
PORT=8000   # optional, defaults to 8000
```

> Get your Gemini API key at [aistudio.google.com](https://aistudio.google.com)

### 4. Start the backend

```bash
npm run dev    # development (with auto-reload)
# or
npm start      # production
```

### 5. Open the app

Visit **[http://localhost:8000](http://localhost:8000)** in your browser.

### 6. Use the app

1. Paste your **GitHub or GitLab personal access token**
2. Select **repositories**, **branches**, and a **date**
3. Click **Fetch Commits**
4. Fill in **Project / Client Name** and **Your Name / Role**
5. Click **Generate Daily Update**
6. Use **Copy Full Report**, **Copy Table**, or **Send via Email** to share

---

## ☁️ Production Deployment

### Backend — Vercel

1. Deploy the Node app (`server.js`) to Vercel
2. Set environment variables in the Vercel dashboard:
   - `GOOGLE_API_KEY` — your Gemini API key
3. Your API endpoint will be:
   ```
   https://your-project.vercel.app/api/generate-report
   ```

### Frontend — Netlify (or any static host)

1. Deploy `index.html` as a static site
2. No environment variables needed — the frontend calls your Vercel backend over HTTPS
3. Update the `API_BASE` URL in `index.html` if your backend hostname changes

---

## 🤝 Contributing

DevLog is **open source** and actively welcoming contributions!

### How to contribute

1. **Fork** the repository
2. **Create a branch** — `git checkout -b feature/your-feature-name`
3. **Commit your changes** — `git commit -m "feat: add your feature"`
4. **Push** — `git push origin feature/your-feature-name`
5. **Open a Pull Request**

### Ideas for contributions

- 🔌 New integrations — Jira, Linear, Bitbucket, Azure DevOps
- 📬 Email delivery — Resend, SendGrid, SMTP support
- 🌍 Localization — multi-language support
- 📊 Analytics — weekly/monthly summaries
- 🐛 Bug fixes and UX improvements
- 📝 Documentation improvements

### Safe contribution guidelines

**Never commit:**
- `.env` or any file containing real API keys or tokens
- Keys or tokens in code, comments, or documentation
- Screenshots or logs containing full tokens or keys

**When opening issues or PRs:**
- Mask any tokens in screenshots — use `ghp_****` format
- Scrub `Authorization` or `x-api-key` headers from logs

---

## 🔧 Troubleshooting

**`500 error — GOOGLE_API_KEY is not configured`**
- Check that `GOOGLE_API_KEY` is set in your `.env` (local) or hosting platform dashboard (production)
- Restart or redeploy after setting it

**`GitHub 404 / "Not Found" when fetching commits`**
- Ensure the repo is in `owner/repo` format (e.g. `pankajmadhikar/generative-ai-learning`)
- Double-check the branch name (`main` vs `master`)
- Confirm the date actually has commits on that branch

**`No commits found but repo is correct`**
- Check for UTC vs local time differences — the date filter uses UTC midnight boundaries
- Verify your token has `repo` read scope

---

## 📄 License

MIT — free to use, modify, and distribute.

---

<div align="center">

**Built by devs, for devs. PRs welcome. ⭐ Star the repo if it saves you time!**

[🔗 Live Demo](https://daily-update-generator.netlify.app/) · [🐛 Report a Bug](https://github.com/pankajmadhikar/generative-ai-learning/issues) · [💡 Request a Feature](https://github.com/pankajmadhikar/generative-ai-learning/issues)

</div>
