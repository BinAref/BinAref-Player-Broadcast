# BinAref Player — Broadcast panel

A private admin panel to compose and publish **broadcast cards** for BinAref
Player. Cards are stored in Supabase (`broadcasts` table); the app reads them
and shows each card at the top of the screen while a video plays, and keeps it
in the notifications (bell) section.

Cards are **structured** — an icon, a title, body text, and any number of
buttons — and the app draws them natively in the player's style (no web view),
so they always render on Windows and Android.

One self-contained file — [`index.html`](index.html). No build, no dependencies.

## Run it

Open `index.html` — locally is simplest and safest (double-click, or serve the
folder with `python -m http.server`).

## First-time setup

⚙️ الإعدادات → the **Project URL** is pre-filled → paste your **service_role
key** (Supabase → Project Settings → API → `service_role`) → حفظ. The key is
saved in your browser only (localStorage).

## Compose a card

Fill the fields (live preview on the right updates as you type):

- **id** — unique. Changing it = a new card for everyone.
- **Title** and **Text**.
- **Icon / image** (optional) — pick from your device; it's embedded in the card.
- **Buttons** — add as many as you like; each has a label and a link (opens in
  the browser when tapped).
- **Platforms** — who sees it (empty = everyone).
- **أقصى إصدار** (`max_version`, optional) — only users on this version *or older*
  see the card. Set it to the version you are superseding on an update card, so
  it stops reaching people who already updated.

The two 🎉 **تحديث** templates are ready to send: each carries a direct-download
button (`releases/latest/download/…`, so the link never needs bumping) and
preselects its platform — Windows gets the installer, Android gets the APK.
Send both to cover everyone.
- **قابل للإغلاق** — show the ✕ close button.
- **إغلاق تلقائي (ث)** — seconds the card stays before auto-hiding.
- **فاصل بين الكروت (ث)** — if several cards are sent (or a batch arrives after
  reconnecting), how long to wait after one closes before the next appears.

Click **🚀 نشر / إرسال**. It's live immediately — viewers watching a video get it
within seconds; offline viewers get it the next time they're online and open a
video. A card shows once per device; re-broadcast by publishing with a new id.

The **الكروت الحالية** dropdown lists every card: click one to load it back into
the form, toggle it on/off (`active`), or delete it.

## ⚠️ Security — the service_role key

`service_role` has full access to your database. This panel never stores it in a
file — only in your browser's localStorage. **Never commit it, and don't enter
it while this page is served publicly.** Use the panel locally. The app itself
never uses this key (it reads with the public read-only anon key).
