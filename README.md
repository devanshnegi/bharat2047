# BHARAT 2047 · Mission Control

An independent, fast, mobile-friendly public tracker following India's nominal GDP journey toward **$47 trillion by 2047**.

- **Live site:** `https://devanshnegi.github.io/bharat2047`
- **How it works:** Google Apps Script (`Code.gs`) remains your automated data engine. Every 3 hours, GitHub Actions fetches `?format=json`, validates the data, and saves `data.json` so GitHub Pages loads instantaneously with zero Apps Script banner and clean WhatsApp/LinkedIn link previews.

---

## Files in this repository

| File | Purpose |
| :--- | :--- |
| `index.html` | Self-contained public dashboard (CSS, JS, Chart.js CDN) reading `./data.json` |
| `.github/workflows/update-data.yml` | Scheduled job (every 3 hours) that fetches and validates `data.json` |
| `og.png` | 1200×630 social share preview image (converted from `og.svg`) |
| `data.json` | Generated automatically by GitHub Actions (do not edit manually) |
| `README.md` | These setup instructions |

---

## Step-by-Step Setup Guide (No Coding Required)

### Step 1: Update your Google Apps Script (`Code.gs`)

1. Open your Google Sheet → **Extensions → Apps Script**.
2. In `Code.gs`, scroll to `function doGet()` and replace **only** the `doGet` function with the new `doGet(e)` code provided (nothing else in `Code.gs` needs to change).
3. Click **Save** (floppy disk icon or `Ctrl+S` / `Cmd+S`).
4. In the top-right, click **Deploy → Manage deployments**.
5. Click the **Edit (pencil)** icon on your existing Web App deployment.
6. Under **Version**, choose **New version** (important: if you don't select *New version*, the `?format=json` change won't go live).
7. Make sure **Execute as** is set to **Me** and **Who has access** is set to **Anyone**.
8. Click **Deploy**, then **copy the Web App URL** (it ends in `/exec`).
9. Quick test: paste that URL into a new browser tab with `?format=json` at the end (for example `https://script.google.com/macros/s/YOUR_ID/exec?format=json`). You should see JSON text starting with `{"generatedAt":...}`.

---

### Step 2: Create `og.png` (for WhatsApp & LinkedIn Previews)

WhatsApp and LinkedIn require a `.png` or `.jpg` image (they do not preview `.svg` files).

1. Take the included `og.svg` file (1200×630).
2. Open a free online converter such as [svgtopng.com](https://svgtopng.com) or [cloudconvert.com/svg-to-png](https://cloudconvert.com/svg-to-png).
3. Upload `og.svg` (ensure output dimensions are **1200 × 630** pixels) and download the converted file as **`og.png`**.

---

### Step 3: Upload Files to GitHub (`devanshnegi/bharat2047`)

1. Go to `https://github.com/devanshnegi/bharat2047` (create the public repository named `bharat2047` if you haven't already).
2. Upload **`index.html`**, **`og.png`**, and **`README.md`**:
   - Click **Add file → Upload files**.
   - Drag in `index.html`, `og.png`, and `README.md`.
   - Click **Commit changes**.
3. Create the workflow file **`.github/workflows/update-data.yml`**:
   - Click **Add file → Create new file**.
   - In the **"Name your file..."** box at the top, type exactly:
     `.github/workflows/update-data.yml`
     *(Typing the `/` slashes automatically creates the `.github` and `workflows` folders!)*
   - Paste the full contents of `.github/workflows/update-data.yml` into the editor.
   - Click **Commit changes…** → **Commit changes**.

---

### Step 4: Add your Apps Script URL as a Repository Variable

1. In your GitHub repo (`devanshnegi/bharat2047`), click the **Settings** tab.
2. In the left sidebar, click **Secrets and variables → Actions**.
3. Click the **Variables** tab (not Secrets — choose **Variables**).
4. Click **New repository variable**.
5. Set:
   - **Name:** `APPS_SCRIPT_URL`
   - **Value:** Paste your copied `/exec` Web App URL from Step 1 (for example `https://script.google.com/macros/s/.../exec` — without `?format=json`, though the workflow handles it either way).
6. Click **Add variable**.

---

### Step 5: Enable GitHub Pages

1. Go to **Settings → Pages** in the left sidebar.
2. Under **Build and deployment → Source**, select **Deploy from a branch**.
3. Under **Branch**, select **`main`** and **`/ (root)`**.
4. Click **Save**.

---

### Step 6: Run the Data Sync Workflow Once

1. Click the **Actions** tab at the top of your repository.
2. In the left list, click **Update Bharat 2047 Data**.
3. Click the **Run workflow** dropdown on the right → click the green **Run workflow** button.
4. Wait ~20–30 seconds and refresh the page until you see a green checkmark ✅.
5. Check your main repository page: you should now see **`data.json`** committed automatically by `github-actions[bot]`.

---

### Step 7: Test on Your Phone & WhatsApp

1. Open `https://devanshnegi.github.io/bharat2047` on your phone (try both Wi-Fi and mobile data, or an incognito tab signed into multiple Google accounts).
2. Paste `https://devanshnegi.github.io/bharat2047` into a WhatsApp message to yourself and wait 2 seconds — you should see the **BHARAT 2047** card with the `og.png` preview image!
   *(Tip: If WhatsApp cached an older link without an image, test with `https://devanshnegi.github.io/bharat2047/?v=1` or inspect with LinkedIn Post Inspector.)*

---

## Troubleshooting

- **Workflow failed with "Invalid payload":** Check your `APPS_SCRIPT_URL` variable and make sure Step 1 deployed a **New version** with **Who has access: Anyone**.
- **Dashboard says "Data could not be loaded":** Make sure Step 6 succeeded and `data.json` exists in your `main` branch. GitHub Pages can take 1–2 minutes after `data.json` is committed to publish.
- **Disclaimer:** Independent tracker, not an official Government of India dashboard.
