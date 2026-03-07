# StockMeta AI

**Bulk metadata generator for stock images & vectors — powered by Google Gemini AI.**

StockMeta AI is a Windows desktop application that automatically generates titles, keywords, and categories for your stock photos and vector files. Export platform-ready CSV files for **Adobe Stock**, **Shutterstock**, and **Freepik** in seconds instead of hours.

---

<img width="1919" height="1016" alt="image" src="https://github.com/user-attachments/assets/56fcf765-a733-4333-af7e-9c6ce3ab0ad3" />

## Download & Install

1. Go to the [**Releases**](../../releases/latest) page
2. Download `StockMetaAI_Setup_x.x.x.exe`
3. Run the installer → follow the wizard
4. Launch **StockMeta AI** from the Start Menu or Desktop shortcut


### System Requirements

| Requirement | Details |
|---|---|
| **OS** | Windows 10 / 11 (64-bit) |
| **RAM** | 4 GB minimum |
| **Disk** | ~80 MB installed |
| **Internet** | Required for metadata generation (Gemini API) and license verification |
| **API Key** | Free Google Gemini API key ([get one here](https://aistudio.google.com/apikey)) |

---

## Getting Started

### 1. Set Up Your API Key

- Open **StockMeta AI** → go to the **Settings** tab
- Paste your [Google Gemini API key](https://aistudio.google.com/apikey) → click **Save Key**
- Your key is stored securely in Windows Credential Manager (never saved to disk as plain text)

### 2. Generate Metadata

- Go to the **Generate** tab
- Click **Browse** → select a folder containing your images
- Choose your target platforms (Adobe Stock, Shutterstock, Freepik)
- Configure file extensions per platform if needed (`.eps`, `.jpg`, `.png`, or `original`)
- Click **Generate Metadata**
- View results in the **Results** tab → click **Save CSV**

### 3. Convert Images (Optional)

- Go to the **Convert** tab
- Select a folder or individual files
- Choose output format (JPG or PNG)
- Click **Convert Images**

---

## Features

### AI-Powered Metadata Generation

- **Multi-Platform CSV Export** — Generate ready-to-upload CSVs for Adobe Stock, Shutterstock, and Freepik, each with the correct platform-specific schema
- **EPS / Vector Support** — Process `.eps` vector files just like raster images — Ghostscript is bundled, no separate installation needed
- **Batch Processing** — Sends up to 5 images per API call, dramatically reducing processing time and API usage
- **Smart Model Selection** — Automatically alternates between multiple Gemini models (`gemini-3-flash-preview`, `gemini-2.5-flash`, `gemini-2.5-flash-lite`) for optimal speed and reliability
- **Accurate Results** — Generates descriptive titles (up to 200 characters), 30–45 relevant keywords, and platform-specific categories
- **Configurable Extensions** — Choose the filename extension (`.eps`, `.jpg`, `.png`, or original) written in the CSV for each platform

### Reliability & Performance

- **Rate Limit Protection** — Built-in delays between batches with automatic exponential backoff when rate limits are hit
- **Circuit Breaker** — Automatically switches to fallback models after repeated rate limits
- **Crash-Safe Checkpoints** — Progress is saved after every batch; if the app closes unexpectedly, it resumes where it left off
- **Cancel & Keep Results** — Stop processing at any time and keep all completed results
- **Retry Failed** — Re-process only the images that failed without re-running everything
- **Non-Blocking UI** — EPS thumbnails render in background threads with loading animations; the app never freezes

### Image Conversion

- **Format Conversion** — Convert between JPG, PNG, and EPS
- **Maximum Quality Output** — JPG at quality 100, PNG lossless
- **EPS Rasterization** — Vector files rendered at native canvas size
- **Transparency Handling** — PNG transparency composited onto white when converting to JPG
- **EXIF Preservation** — Metadata carried over to output files
- **Safe Output** — Automatic `_1`, `_2` suffixes prevent overwriting existing files

### General

- **Auto-Updater** — Get notified when a new version is available and update with one click
- **Secure API Key Storage** — Keys stored in Windows Credential Manager, never in config files
- **Dark / Light / System Theme** — Customizable appearance
- **Subscription Licensing** — Email-based login with device binding (1 account = 1 device) and 24-hour offline grace period; all login screens appear inline in the main window
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

### Input (Image Conversion)

`.jpg`, `.jpeg`, `.png`, `.eps`

### Output (Image Conversion)

`.jpg`, `.png`

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

## CSV Output Formats

### Adobe Stock

| Column | Description |
|---|---|
| Filename | Asset filename |
| Title | Descriptive title (max 200 characters) |
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
| API Key | Windows Credential Manager (via Settings tab) |
| App preferences | `%APPDATA%\MetadataGenerator\config.json` |
| Log files | `%APPDATA%\MetadataGenerator\logs\app.log` |
| Checkpoints | `<output_folder>/<csv_name>_checkpoint.json` (auto-deleted on completion) |

Configurable options include:
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


## Troubleshooting

| Issue | Solution |
|---|---|
| **"Ghostscript not found"** | Reinstall the app — Ghostscript is bundled in the installer |
| **EPS thumbnails not loading** | Ensure the app installed correctly; check logs at `%APPDATA%\MetadataGenerator\logs\` |
| **API key not working** | Verify your key at [Google AI Studio](https://aistudio.google.com/apikey); make sure it has Gemini API access |
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
