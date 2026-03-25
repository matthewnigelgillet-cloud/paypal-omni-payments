# Omni Payments Strategy — Google Slides Generator

Generates a single-slide "Omni Payments Ambition" deck via the Google Slides API.

---

## Prerequisites

- Node.js 18+
- A Google account with access to Google Drive / Slides

---

## 1 — Enable the Google Slides API

1. Go to [console.cloud.google.com](https://console.cloud.google.com).
2. Create a new project (or select an existing one).
3. Navigate to **APIs & Services → Library**.
4. Search for **Google Slides API** and click **Enable**.

---

## 2 — Create OAuth 2.0 credentials

1. Go to **APIs & Services → Credentials**.
2. Click **+ Create Credentials → OAuth client ID**.
3. Application type: **Desktop app** (or "Web application" if you already have one).
4. Give it any name, click **Create**.
5. Click **Download JSON** on the credential that appears.
6. Rename the downloaded file to `credentials.json` and place it in this directory.

> **OAuth consent screen** — if prompted, configure it in **APIs & Services → OAuth consent screen**.
> Add yourself as a Test User while the app is in testing mode.

---

## 3 — Install dependencies

```bash
npm install
```

---

## 4 — Run the script

```bash
node script.js
```

**First run:** the script will print an authorisation URL. Open it in your browser, approve access, and paste the code back into the terminal. A `token.json` file is saved automatically for subsequent runs.

**Subsequent runs:** the cached token is used; re-authorisation is only needed if the token expires or is revoked.

---

## 5 — Output

The script prints the presentation URL on success:

```
Presentation created successfully.
URL: https://docs.google.com/presentation/d/<id>/edit
```

Open the link to view and share your slide.

---

## Troubleshooting

| Error | Fix |
|-------|-----|
| `credentials.json not found` | Download credentials from Google Cloud Console (step 2). |
| `Authentication error (401)` | Delete `token.json` and re-run — you will be prompted to re-authorise. |
| `Rate-limited (429)` | The script retries automatically with exponential backoff (up to 4 attempts). |
| `redirect_uri_mismatch` | In Cloud Console, add `urn:ietf:wg:oauth:2.0:oob` or `http://localhost` as an authorised redirect URI for your OAuth client. |

---

## Slide design

| Element | Value |
|---------|-------|
| Slide size | 720 × 405 pt (10 × 5.625 in, native 16:9) |
| Background | White `#FFFFFF` |
| Heading | Century Gothic 26 pt bold, black |
| Continuum line | 4 pt, `#0070E0`, bidirectional fill arrows |
| Anchor labels | Century Gothic 10 pt bold, `#003087` |
| Position marker | Filled circle `#0070E0`, 20 % from left |
| Tick marks | 1.5 pt at 25 %, 50 %, 75 % |
| Current state label | Century Gothic 9 pt italic, `#767676` |
