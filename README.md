# PVF Reorder Calculator

A browser-based inventory replenishment tool for PVF (pipe, valve, fitting) distributors. Drop in an Excel inventory export, get back a vendor-ready buy list sized to a configurable months-of-demand target.

## What it does

- **Auto-detects UOM** (each vs. C/per-100 pricing for pipe) by cross-checking the system's extended amounts against quantities
- **Calculates reorder quantities** to bring each stocked SKU to a 3-month position (adjustable)
- **Smart filters** skip low-value lines and slow-moving cheap items that aren't worth the PO handling
- **Rounds up to PPQ** so recommendations match how vendors ship
- **Exports CSV** for sending to vendors or importing back into your ERP

All processing happens **client-side in the browser** — no file ever leaves your machine. Safe to host publicly.

## Expected input columns

The tool reads these fields from the Excel export:
`Alt Code`, `Description`, `Tier`, `Avg Dmd Amt`, `On Hand`, `On PO`, `On BO`, `PPQ`, `Per Qty`, `Avg Cost`, `Ext OHB Amt`, `Ext Avail Amt`, `Ext Open PO Amt`, `Prod Cat Desc`, `Primary Vendor`, `Lead Time`, `Bin Location`

---

## Deploying to Render

**Prerequisites:** A free GitHub account (github.com) and a free Render account (render.com).

### 1. Create a GitHub repo

1. On github.com, click the **+** icon (top right) → **New repository**
2. Name it something like `pvf-reorder-calculator`
3. Set it to **Private** (recommended — this is a business tool)
4. Don't initialize with a README (you're adding your own files)
5. Click **Create repository**

### 2. Upload the files to the repo

On the new empty repo page, click **uploading an existing file** (it's a link in the quick setup section), then drag these two files in:
- `index.html`
- `README.md`

Commit directly to `main`.

### 3. Deploy on Render

1. Sign up at **render.com/register** — use "Sign up with GitHub" so the connection is automatic
2. From the Render dashboard, click **New +** → **Static Site**
3. Find your `pvf-reorder-calculator` repo in the list and click **Connect**
4. Fill in the form:
   - **Name**: `pvf-reorder` (this becomes your URL: `pvf-reorder.onrender.com`)
   - **Branch**: `main`
   - **Root Directory**: *leave blank*
   - **Build Command**: *leave blank* (no build step needed)
   - **Publish Directory**: `.` (a single period — means the repo root)
5. Click **Create Static Site**
6. Wait ~30 seconds for the first deploy to finish

Your tool is now live at `https://pvf-reorder.onrender.com`.

### 4. (Optional) Custom domain

If you own a domain (e.g., `pvfinstitute.com`), you can point a subdomain like `reorder.pvfinstitute.com` at your Render site:

1. In Render: **Settings** → **Custom Domains** → **Add Custom Domain**
2. Enter your subdomain
3. Render gives you DNS records to add at your domain registrar
4. Free SSL cert is auto-provisioned once DNS propagates (usually <1 hour)

### Updating the tool

Any commit pushed to the `main` branch triggers an auto-redeploy. You can edit `index.html` directly on GitHub (click the file → pencil icon → commit) and the live site updates in about 30 seconds.

---

## Local use

If you ever want to use it offline, just download `index.html` and double-click to open in any browser. Works identically — the hosted version is the same file.
