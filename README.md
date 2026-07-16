# BinAref Player — Broadcast panel

A private admin panel to write, preview, and publish **broadcast cards** for
BinAref Player. Cards are stored in Supabase (`broadcasts` table); the app reads
them and shows each card at the top of the screen while a video plays.

One self-contained file — [`index.html`](index.html). No build, no dependencies.

## Run it

Open `index.html` — locally is simplest and safest:

- **Double-click `index.html`**, or serve the folder: `python -m http.server` →
  open `http://localhost:8000`.

## First-time setup

1. Click **⚙️ الإعدادات**.
2. **Project URL** is pre-filled.
3. Paste your **service_role key** (Supabase → Project Settings → API →
   `service_role`) → **حفظ**. The dot turns green. The key is saved in your
   browser only (localStorage).

## Author a card

- **Three tabs — HTML / CSS / JS.** Write each part in its tab. The panel wraps
  them into one document. The preview updates live.
- **Size & duration are set inside the code** — the first line of the CSS tab:
  `/* @card 380 x 150 | 10s */` (width × height, and seconds shown). Edit those
  numbers; the preview and the published card use them.
- **Icon / image from your device** — click **＋ أضف أيقونة**, pick an image, and
  reference it in the code with `{{icon}}` (the starter HTML has
  `<img src="{{icon}}">`). The image is embedded into the card, so it works on
  every device. Keep it small (< ~800 KB).
- **Bridge:** `BinAref.close()` closes the card, `BinAref.open('https://…')`
  opens a link. Plain `<a href>` links open in the browser too.

Only three settings live outside the code:

- **Platforms** — which OSes see it (empty = everyone).
- **قابل للإغلاق** — show the app's ✕ close button.
- **نشِط (active)** — see below.

Click **🚀 نشر / إرسال** to publish (live immediately, no app update), **👁️ عرض**
to refresh the preview, or **نسخ JSON** to copy the card.

## `active` — how it behaves

- **active = on:** anyone who opens a video (and hasn't seen this card yet) gets it.
- **active = off:** it stops appearing for everyone — even people who never saw
  it, even if they're online.
- **turn it back on:** people who already saw it will **not** see it again
  (each device remembers what it showed); people who never saw it will now get it.
- To deliberately re-show something to everyone, publish it with a **new id**.

## Manage cards

The **الكروت الحالية** table lists every card: **تحميل** loads it back into the
tabs (HTML/CSS/JS + icon), **إيقاف/تشغيل** toggles `active`, **حذف** removes it.

## ⚠️ Security — the service_role key

`service_role` has **full access** to your database. This panel never stores it
in a file — only in your browser's localStorage at runtime.

- **Never commit it.**
- **Don't enter it while this page is served publicly.** Use the panel locally.
- **مسح المفتاح** wipes it from the browser.

The app itself never uses this key — it reads with the public read-only anon key.
