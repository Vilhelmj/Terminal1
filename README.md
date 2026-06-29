# Terminal1

A single-file web app (`index.html`) for your Android phone. It uses the rear
camera to scan GS1‑128 shipping‑label barcodes, extracts **only the SSCC**
(Application Identifier `(00)`, the 18‑digit logistic‑unit serial), de‑duplicates,
keeps a running list that survives app restarts, and lets you send all the numbers
by **Email / Share / CSV / Copy** when you're done.

It deliberately ignores the other barcodes on a pallet label (e.g. the `(02)…(37)…`
GTIN‑and‑count barcode) — those never produce a number in the list.

## Why it must be hosted on HTTPS

Phone browsers only allow camera access on a **secure (https://) page**. Opening the
file directly from a folder or an email attachment will *not* start the camera (you
can still type SSCCs in by hand). The free, reliable way to get an https URL is
GitHub Pages.

## Put it online in ~2 minutes (GitHub Pages)

1. On github.com create a **new public** repo, e.g. `sscc-scanner`
   (Pages on a private repo needs a paid plan — use a public repo with just this file).
2. Upload `index.html` to the repo root (drag‑and‑drop in the GitHub web UI is fine),
   commit to the `main` branch.
3. Repo → **Settings** → **Pages** (left sidebar).
4. Under **Build and deployment → Source** pick **Deploy from a branch**.
5. Branch: **main**, Folder: **/ (root)** → **Save**.
6. Wait ~1 minute, then open the published URL on your phone:
   `https://<your-username>.github.io/sscc-scanner/`

Bookmark that URL / add it to your home screen. The scanned list is stored on the
phone, so you can close and reopen it without losing scans.

## Using it

- Tap **Start camera**, point the box at the SSCC barcode. A high beep + buzz = added;
  a low buzz + "Already scanned" = duplicate (it won't add the same SSCC twice).
- 🔦 toggles the flashlight (if your camera supports it).
- **Type** an SSCC manually if a barcode is damaged.
- When finished: **Share** (sends a CSV file via Android's share sheet — best for long
  lists), **CSV** (downloads a file), **Email** (opens your mail app pre‑filled — best
  for short lists), or **Copy**.
- Each row has a **×** to delete it; **Clear all** wipes the list (asks first).

## Notes

- Primary decoder is the phone's built‑in **BarcodeDetector** (Android Chrome). On
  devices/browsers without it (e.g. some iPhones), it auto‑loads the **ZXing** library
  from a CDN as a fallback — so the fallback path needs internet the first time.
- SSCC check digits are validated, so misreads and typos are rejected.
