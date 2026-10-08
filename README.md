# PageBrief — AI Web Scraper

A small full-stack app that accepts a public webpage URL, extracts readable HTML content, and uses the Google Gemini API to generate a short summary.

## Stack

- React + Vite
- Node.js + Express
- Cheerio for HTML parsing
- Google Gemini API

## Project structure

```text
.
├── client/
│   ├── src/
│   │   ├── main.jsx
│   │   └── styles.css
│   ├── index.html
│   └── package.json
├── server/
│   └── index.js
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

## Run locally

### 1. Install dependencies

From the project root:

```bash
npm install
cd client
npm install
cd ..
```

### 2. Configure the API key

Create a `.env` file in the **project root** (not inside `client`):

```env
PORT=5000
GEMINI_API_KEY=your_gemini_api_key
GEMINI_MODEL=gemini-2.5-flash
```

Get a Gemini API key from Google AI Studio. Keep the key on the server and never put it in the React app.

### 3. Start the app

```bash
npm run dev
```

The frontend runs on Vite's local port and the API runs on `http://localhost:5000`.

## API

`POST /api/summarize`

Request:

```json
{
  "url": "https://example.com/article"
}
```

Response:

```json
{
  "title": "Example article",
  "url": "https://example.com/article",
  "summary": "..."
}
```

## Notes

This scraper intentionally handles basic server-rendered HTML. It does not try to bypass bot protection or execute client-side JavaScript. Some websites may block automated requests or require JavaScript to display their content.

For production, add rate limiting, request allow/block rules, stronger SSRF protection, logging, and authentication before exposing the scraper publicly.

## Deployment

The client and server can be deployed separately.

### Backend

Deploy the project root to a Node.js host such as Render. Set:

```text
GEMINI_API_KEY=...
GEMINI_MODEL=gemini-2.5-flash
PORT=5000
```

Start command:

```bash
node server/index.js
```

### Frontend

Deploy the `client` folder to Vercel or another static host.

Set the frontend environment variable:

```text
VITE_API_URL=https://YOUR-BACKEND-URL
```

Then run the normal Vite build command:

```bash
npm run build
```

Do not commit `.env` or expose the Gemini key in frontend code.
