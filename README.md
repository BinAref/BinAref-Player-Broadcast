# BinAref Player — Broadcast panel

A private admin panel to write, preview, and publish **broadcast cards** for
BinAref Player. Cards are stored in Supabase (`broadcasts` table); the app reads
them and shows each card at the top of the screen while a video plays.

Everything is one self-contained file — [`index.html`](index.html). No build, no
dependencies.

## Run it

Just open `index.html` — locally is simplest and safest:

- **Double-click `index.html`** (opens in your browser), **or**
- serve the folder: `python -m http.server` → open `http://localhost:8000`.

You can also make this repo temporarily public + host it (GitHub Pages, etc.),
edit, then make it private again — but see the security note below first.

## First-time setup

1. Click **⚙️ الإعدادات**.
2. **Project URL** is pre-filled (`https://ijgqmjgllwtcjziyrgvc.supabase.co`).
3. Paste your **service_role key** — Supabase → Project Settings → API →
   `service_role`. Click **حفظ**.

The key is saved in your browser only (localStorage) and is sent only to
Supabase. The connection dot turns green when set.

## Publish a card

1. Enter a unique **id** (changing the id = a new card for everyone).
2. Write the card in the **HTML/CSS/JS** editor — the preview updates live.
   - Keep the page background transparent so only the card shows.
   - `BinAref.close()` closes the card; `BinAref.open('https://…')` opens a link.
3. Set size, duration, platforms, active.
4. Click **🚀 نشر / إرسال**. It's live immediately — no app update.

Use **نسخ JSON** to copy the card as JSON (if you'd rather publish it elsewhere).

The **الكروت الحالية** table lists every card: load one back into the editor,
toggle it on/off (`active`), or delete it.

## ⚠️ Security — the service_role key

`service_role` has **full access** to your database and bypasses row-level
security. Therefore:

- **Never commit it** to this (or any) repo. This panel never stores it in a
  file — only in your browser's localStorage at runtime.
- **Don't enter it while this page is served publicly on the internet.** Use the
  panel **locally**. If you host it publicly to edit, do it without the key, or
  take the page down again afterwards.
- Use **مسح المفتاح** to wipe the key from the browser when done on a shared
  machine.

The app itself never uses this key — it reads with the public read-only anon key.
This panel is only for you (the admin) to author cards.
