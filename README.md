# StockMeta AI v3.7.1

**Bulk metadata generator for stock images & vectors — powered by Google Gemini and Anthropic Claude APIs.**

StockMeta AI is a Windows desktop application that automatically generates titles, keywords, and categories for your stock photos and vector files. Export platform-ready CSV files for **Adobe Stock**, **Shutterstock**, and **Freepik** in seconds instead of hours.

---

<img width="1919" height="1021" alt="image" src="https://github.com/user-attachments/assets/00551836-6c97-4a50-b133-fcf4066bd91c" />

## Download & Install

1. Go to the [**Releases**](../../releases/latest) page
2. Download `StockMetaAI_Setup_3.7.0.exe`
3. Run the installer → follow the wizard
4. Launch **StockMeta AI** from the Start Menu or Desktop shortcut

> **No Python or Adobe Illustrator setup required.** Ghostscript and Inkscape 1.4.4 are bundled for EPS → SVG conversion.

### System Requirements

| Requirement | Details |
|---|---|
| **OS** | Windows 10 / 11 (64-bit) |
| **RAM** | 4 GB minimum |
| **Disk** | Up to ~1.2 GB installed (includes vector conversion runtimes) |
| **Internet** | Required for metadata generation (selected Gemini or Claude API) and license verification |
| **API Key** | A Google Gemini key or an Anthropic Claude API key with API billing enabled |

---

## How to Update (v3.5.2+)

The application **automatically checks for updates on startup**. If a newer version is deployed, a dialog box will prompt you to download the update directly inside the app. Clicking **Yes** will elegantly download the file in the background, trigger the Windows Admin (UAC) prompt, and automatically install the new update for you. You can optionally manually click **Check for Updates** in the **Settings** page.

*(Note: Users on older versions where this bug existed may need to manually download the new setup from the Releases page).*

---

## Getting Started

### 1. Choose Your Provider, Key, and Model

- Open **StockMeta AI** → **Settings** → choose **Google Gemini** or **Anthropic Claude**.
- Enter the selected provider's key and click **Save Key**. Each provider keeps its own key in Windows Credential Manager. **Show** and **Delete Key** affect only that provider.
- **Gemini:** Get a key from [Google AI Studio](https://aistudio.google.com/apikey). Leave **AI Model** on automatic selection for model rotation, or enter a supported model ID.
- **Claude:** Create a key in [Anthropic Console](https://platform.claude.com/settings/keys) and configure API billing. Claude chat subscriptions do not include API billing. Click **Refresh Models** or **Test Connection**, select an available model (or type its exact ID), then **Save Settings**.
- With no saved Claude selection, StockMeta discovers models and prefers the newest available image-capable Haiku, then Sonnet. The resolved ID is saved and used for the entire job. No Claude model ID is hardcoded.

Connection tests only query model availability; they do not generate content or confirm remaining generation credits. Switching providers preserves both keys and model preferences. A running job keeps the settings it started with.

### 2. Generate Metadata

- Go to the **Analyze** tab
- Click **Browse** → select a folder containing your images
- Choose your target platforms (Adobe Stock, Shutterstock, Freepik)
- Configure file extensions per platform if needed (`.eps`, `.svg`, `.jpg`, `.png`, or `original`)
- Click **Generate Metadata**
- View results in the **Results** tab → click **Save CSV**

### 3. Prepare Files (Optional)

- Go to the **Prepare** tab
- Select a folder or individual files
- Choose output format (JPG, PNG, or SVG)
- Click **Prepare Files**

---

## Features

### AI-Powered Metadata Generation

- **Gemini or Claude** — Choose the API provider in Settings for generation, retries, regeneration, and Pro keyword optimization. Both use the same stock platform rules and CSV formats.
- **Readable Settings Menus** — Provider and model dropdowns have opaque dark backgrounds.
- **Dual-Layer IP & Policy Risk Detection** — Combines visual checks from the selected provider with shared local metadata rules to flag restricted content, brands, and proprietary IP before export.
- **Dynamic Platform Optimization** — Conserves API tokens and halves generation time by strictly generating schemas and rules only for the platforms you have checked.
- **Multi-Platform CSV Export** — Generate ready-to-upload CSVs for Adobe Stock, Shutterstock, and Freepik, each with the correct platform-specific schema
- **AI Autofix & Regeneration (Pro)** — Intelligently review and regenerate missing or semantically poor keywords and titles using one-click AI-assisted Autofix functionality directly from the Results grid.
- **Advanced Results Review** — A completely overhauled Results Page featuring platform-tabbed views, sophisticated bulk/per-file export filtering, and persistent local session states.
- **Vector Support** — Process `.eps` and `.svg` vector files just like raster images; Ghostscript is bundled for EPS and Qt handles SVG
- **Batch Processing** — Sends up to 5 images per API call, dramatically reducing processing time and API usage
- **Gemini Automatic Model Rotation** — Automatic Gemini selection uses primary models `gemini-3.8-flash`, `gemini-3.7-flash`, `gemini-3.6-flash`, and `gemini-3.5-flash`, with two passes before `gemini-3.5-flash-lite` and `gemini-3.1-flash-lite` fallbacks. Recent model health influences order. Manual Gemini selection and Claude jobs use a fixed model.
- **Accurate Results** — Generates Adobe titles containing 15–20 words, 100–150 characters, and the required phrase "Vector Design and Illustration," plus 30–45 relevant keywords and platform-specific categories
- **Configurable Extensions** — Choose the filename extension (`.eps`, `.svg`, `.jpg`, `.png`, or original) written in the CSV for each platform

### Reliability & Performance

- **Rate Limit Protection** — Built-in delays between batches with automatic exponential backoff when rate limits are hit
- **Provider-Specific Recovery** — Gemini retains its existing circuit breaker and fallback models. Claude retries transient failures with bounded backoff; credential, billing, permission, and unavailable-model errors stop the job. Errors never switch providers.
- **Crash-Safe Checkpoints** — Progress is saved atomically after batches with provider/model provenance. To resume a job, keep its original provider/model settings; cancelled/skipped images can be processed again.
- **Cancel & Keep Results** — Stop processing at any time and keep all completed results
- **Retry Failed** — Re-process only the images that failed without re-running everything
- **Non-Blocking UI** — EPS and SVG thumbnails render in background threads with loading animations; the app never freezes

### Image Conversion

- **Format Conversion** — Convert raster/vector inputs to JPG/PNG and EPS to SVG 1.1
- **Adobe Technical Preflight** — RGB, one `(0,0)` artboard, 15–65 MP, 45 MB maximum, outlined text, editable paths, and no raster/linked/external/hidden content
- **Safe Vector Publishing** — Failed validation leaves no output file; successful files report “Adobe technical checks passed”
- **No Illustrator Required** — Bundled Ghostscript and Inkscape 1.4.4 always handle EPS → SVG
- **Artboard Alignment** — Conversion preserves the EPS page and internal margins while restricting PDF-import background bleed to the exact SVG artboard
- **Maximum Quality Output** — JPG at quality 100, PNG lossless
- **Vector Rasterization** — EPS files are rendered via Ghostscript and SVG files via Qt
- **Transparency Handling** — PNG/EPS/SVG transparency is composited onto white when converting to JPG
- **EXIF Preservation** — Metadata carried over to output files
- **Safe Output** — Automatic `_1`, `_2` suffixes prevent overwriting existing files

### General

- **In-App Media Deletion** — Permanently toss rejected/IP-flagged images straight from the grid. Purges disk files and memory logs simultaneously.
- **Custom UI Overlays** — System popups and messagebox alerts have been replaced by visually appealing, blurred-background custom overlay dialogs for a cohesive user experience.
- **Auto-Updater** — Get notified when a new version is available and update with one click
- **Secure API Key Storage** — Keys stored in Windows Credential Manager, never in config files
- **Dark / Light / System Theme** — Customizable appearance
- **Subscription Licensing** — Email-based login with distinct **Free** and **Pro** tiers, device binding (1 account = 1 device), and 24-hour offline grace period.
- **Detailed Logging** — Rolling log files for troubleshooting (`%APPDATA%\MetadataGenerator\logs\`)

---

## Supported File Formats

### Input (Metadata Generation)

| Format | Extensions |
|---|---|
| JPEG | `.jpg`, `.jpeg` |
| PNG | `.png` |
| WebP | `.webp` |
| GIF | `.gif` |
| BMP | `.bmp` |
| EPS (Vector) | `.eps` |
| SVG (Vector) | `.svg` |

### Input (Image Conversion)

`.jpg`, `.jpeg`, `.png`, `.eps`, `.svg`

### Output (Image Conversion)

`.jpg`, `.png`, `.svg` (EPS input only)

Vector technical checks follow Adobe's [submission requirements](https://helpx.adobe.com/stock/contributor/submit-your-content/submit-vectors/technical-requirements-for-vector-submissions.html). A passed result confirms file-level technical readiness, not guaranteed Adobe Stock acceptance; moderation also evaluates artistic and legal quality.

---

## CSV Output Formats

### Adobe Stock

| Column | Description |
|---|---|
| Filename | Asset filename |
| Title | Concise, buyer-friendly title (15–20 words and 100–150 characters) containing "Vector Design and Illustration" |
| Keywords | Comma-separated keywords (max 49) |
| Category | Adobe Stock category number (1–21) |
| Releases | Model/property releases |

### Shutterstock

| Column | Description |
|---|---|
| Filename | Asset filename |
| Description | Detailed description |
| Keywords | Comma-separated keywords |
| Categories | Shutterstock categories |
| *Illustration* | Optional (toggle in Settings) |
| *Mature Content* | Optional (toggle in Settings) |
| *Editorial* | Optional (toggle in Settings) |

### Freepik

| Column | Description |
|---|---|
| File name | Asset filename |
| Title | Descriptive title (max 100 characters) |
| Keywords | Comma-separated keywords |

---

## Adobe Stock Categories

| # | Category | # | Category |
|---|---|---|---|
| 1 | Animals | 12 | Lifestyle |
| 2 | Buildings and Architecture | 13 | People |
| 3 | Business | 14 | Plants and Flowers |
| 4 | Drinks | 15 | Culture and Religion |
| 5 | The Environment | 16 | Science |
| 6 | States of Mind | 17 | Social Issues |
| 7 | Food | 18 | Sports |
| 8 | Graphic Resources | 19 | Technology |
| 9 | Hobbies and Leisure | 20 | Transport |
| 10 | Industry | 21 | Travel |
| 11 | Landscape | | |

---

## Settings & Configuration

| Setting | Location |
|---|---|
| Gemini and Claude API keys | Separate entries in Windows Credential Manager (via Settings) |
| AI provider and per-provider models | Settings → AI Provider / AI Model → Save Settings |
| App preferences | `%APPDATA%\MetadataGenerator\config.json` |
| Log files | `%APPDATA%\MetadataGenerator\logs\app.log` |
| Checkpoints | `<output_folder>/<csv_name>_checkpoint.json` (auto-deleted on completion) |

Configurable options include:

- AI provider and separate Gemini/Claude model preferences
- Target platforms and file extension per platform
- Output folder for CSVs and converted images
- Theme (Dark / Light / System)
- Shutterstock optional columns (Illustration, Mature Content, Editorial)
- Image conversion input mode (folder vs. individual files) and output format

---

## Updating

StockMeta AI checks for updates automatically on launch. When a new version is available:

1. A dialog appears showing the changelog
2. Click **Update** to download the new installer
3. The installer launches automatically — follow the wizard to complete the update

You can also check manually from **Settings** → **Check for Updates**.

---

## Subscription & Activation

StockMeta AI requires an active subscription to use.

1. Launch the app — the **Sign In** screen appears directly in the main window
2. Enter your registered email address → click **Send Code** → a 6-digit verification code is sent to your inbox
3. Enter the code → click **Verify** → the app verifies your subscription and binds to your device
4. On subsequent launches, sign-in is automatic (session persists)
5. If you go offline, the app continues to work for up to **24 hours** using cached verification
6. Your account is bound to one device — attempting to use it on a second device shows a "Device Mismatch" error

Your account email and subscription status are displayed in **Settings** → **Subscription**.

To buy or renew a subscription, click the **Contact Us on Telegram** button shown on status screens, or visit **[t.me/StockMetaAIBot](https://t.me/StockMetaAIBot)**.

---

## Troubleshooting

| Issue | Solution |
|---|---|
| **"Ghostscript not found"** | Reinstall the app — Ghostscript is bundled in the installer |
| **Vector thumbnails not loading** | Ensure the app installed correctly; check logs at `%APPDATA%\MetadataGenerator\logs\` |
| **API key not working** | Select the matching provider in Settings, save its key, and click Test Connection. For Claude, also check Console API billing and model access. |
| **Claude model unavailable or retired** | In Settings choose Claude → Refresh Models → select a replacement → Save Settings. |
| **Checkpoint provider/model mismatch** | Restore the job's original provider/model, or select another output folder to start a new job. |
| **Rate limit errors (429)** | The app handles these automatically with backoff; if persistent, wait a few minutes or use a different API key |
| **Subscription expired** | Contact us at [t.me/StockMetaAIBot](https://t.me/StockMetaAIBot) to renew |
| **Device mismatch** | Your account is bound to another device — contact support to reset |
| **App won't start after update** | Uninstall → reinstall from the latest release |
| **CSV is empty** | Check the Results tab — only successful results are written to CSV; failed images are shown but excluded |

For persistent issues, check the log file at:
```
%APPDATA%\MetadataGenerator\logs\app.log
```

---

## License

StockMeta AI is proprietary software distributed under a subscription license. Unauthorized redistribution is prohibited.

---

**Made by [VibeDev Studio](https://github.com/VibeDev-Studio)**
