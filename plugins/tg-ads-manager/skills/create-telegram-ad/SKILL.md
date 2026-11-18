---
name: create-telegram-ad
description: Create a new Telegram ad safely through TG Ads Manager — text, link, targeting (channels, bots, users, search), picture or video, CPM and budget. Use when the user wants to launch, make, set up or copy an ad, e.g. "yangi reklama ochib ber", "создай объявление", "make an ad like my best one".
---

# Create an ad

A new ad is a real ad on Telegram, and its budget moves from the cabinet balance to the ad.

## Steps

1. Cabinet: if not named, call `list_cabinets` and confirm which one. Note its currency.
2. Rules: call `get_ad_form_rules` with `cabinetId`. Use only the fields, targeting options and
   text limits it returns. If it says the form is still being read, tell the user to try again in
   a few minutes and stop.
3. Starting from an existing ad? Call `create_similar_ad` with its `adId`. It returns a prepared
   form (nothing is sent); fill in CPM and budget with the user.
4. Gather from the user, asking only for what is missing: the text, the link (https://), the
   target type (channels, bots, users or search), the targets, CPM and starting budget.
   Optional: `get_draft_market_price` shows the typical CPM for this kind of ad — show it as a
   plain figure or range, nothing more.
5. Check the text and link: call `check_ad` with `cabinetId`, `text`, `promoteUrl` and
   `targetType`. If Telegram objects, show its words and fix the field with the user. Repeat until
   it says Telegram accepts the fields.
6. Check targets — always when targeting channels or bots by name: call `check_targets` with
   `cabinetId`, the `field` (for example `channels` or `bots`) and up to 10 `names` per call.
   Drop every name Telegram refuses and tell the user which ones and Telegram's reason.
7. Picture or video (optional):
   - In Claude: call `open_media_upload` with `cabinetId` (kind `ad_media`, or `promote_photo`
     for a website link picture). Give the user the link; it works 15 minutes for one file.
   - After the user says it is uploaded, call `get_media_upload` with the `uploadId`. If it says
     waiting or uploading, tell the user and wait for them; do not loop.
   - Use the returned `mediaId` (or `websitePhotoId` for promote_photo) in the form.
   - `attach_media` is only for apps that pass an attached file (ChatGPT); do not use it in Claude.
8. Money check: call `preview_topup` with `cabinetId` and `amounts: ["<budget>"]` to show the
   balance after it and whether it is more than the balance.
9. Show a summary table (cabinet, text, link, targets, CPM, budget with currency, started or
   stopped) and get a clear yes.
10. Call `create_ad` with `cabinetId` and the `form`. Keep `active: false` (created stopped)
    unless the user explicitly said to start it now.

## After creating

- Tell the user Telegram reviews every new ad before it shows; the ad appears in `list_ads`
  after the next sync.
- If `create_ad` says the same form was already sent and not sent again, do not repeat it.
  Ask whether they really want a second ad; only on a yes call again with `sendAgain: true`.
- If it is still being sent, say so and stop (see `tg-ads-basics`).
