# AniManxwa subscription bot service

Create a separate Render **Web Service** from this repository. Do not copy the existing `bot.js` from the API repository; this service keeps its webhook isolated and shares only the MongoDB `animanxwa.dev` collection with the app.

## Environment settings

- `BOT_TOKEN`: a fresh token from BotFather (the previously pasted token must be revoked).
- `MONGODB_URI`: same MongoDB cluster/connection string as AniManxwa API.
- `WEBHOOK_SECRET`: generate a long random secret.
- `PUBLIC_URL`: this web service's public HTTPS URL.
- `TG_ADMINS`: comma-separated Telegram numeric IDs; includes `7797502113` by default.
- `PAYMENT_TEXT`: payment instructions/card information, set privately in Render. It is not in this repo.
- `PAYMENT_PHOTO`: optional HTTPS image URL for payment instructions.
- `PROFILE_URL`: defaults to the existing GitHub Pages Profile route.

The checkout stores Telegram IDs in `telegramUsers`, receipts/decision states in `subscriptionRequests`, and writes approved expiry timestamps to the existing `dev` collection. An admin approves/rejects each proof in Telegram; the bot asks the approving admin for the duration in days.

Start payload format is `obuna_<app-id>` (e.g. `https://t.me/AniManxwaBot?start=obuna_123456789012345`). Configure the app's Obuna link to include its local ID in this format.

## Security

The bot token was pasted into a chat. Revoke it with BotFather immediately; never commit tokens, payment-card details, MongoDB credentials, or webhook secrets. Configure them as Render environment secrets only. Configure the API's old `BOT_TOKEN` to a different token or remove it if the existing upload bot should not own this new bot's webhook.
