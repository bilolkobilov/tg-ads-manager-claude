---
name: ads-daily-check
description: Morning or daily check of Telegram ads in TG Ads Manager. Use when the user asks how their ads are doing, for today's or this week's results, spend, views, clicks, CTR or CPA, which ads work best or worst, which budgets run out soon — e.g. "reklamalarim qanday?", "как дела с рекламой?", "show yesterday's stats".
---

# Daily check: how are my ads doing

Read-only. Nothing here changes an ad.

## Steps

1. Call `list_cabinets`. Note each phone's id, each cabinet's id, name, currency and balance.
   If the user named one cabinet, keep only it.
2. Choose the period from the request: `today`, `7d`, `30d`, `this_month`, `last_month`, or a
   range `YYYY-MM-DD..YYYY-MM-DD`. "Yesterday" is a range of that one day. Default: `today`,
   and for a morning check also `7d` for context.
3. Overview: call `get_dashboard` with `phoneId` (and `cabinetId` for one cabinet) and the period.
   It returns balance and money in ads per currency, views, clicks, actions, CTR, spend, the
   period before, ad counts by status, ads whose budget runs out soon, and the top ads.
4. Ads: call `list_ads` with `cabinetId` and the same `period`. It is sorted by spend and paged;
   read the first page only unless the user asks for more. Use `status: "Active"` to see only
   running ads.
5. Only if the user asks about one ad in depth, call `get_ad_stats` with its `adId` and period.
6. If any ad is declined, `list_declined_ads` gives Telegram's own reason for each.

## What to look at

- Spend and results (views, clicks, actions) against the period before.
- CTR (clicks per 100 views) and CPA (cost of one action) where the tool gives them.
- Ads whose budget runs out soon, and active ads with no views in the period.
- Declined ads and their reason.

## How to present

Start with two or three sentences: total spend, the main change against the period before,
and anything that needs action today. Then one small table, at most ten rows:

| Ad | Status | Views | Clicks | CTR | Spend | CPA | Budget left |
|----|--------|-------|--------|-----|-------|-----|-------------|

- Money with its currency (EUR, Gram or Stars). Never add up different currencies.
- Say which period and that days are UTC days.
- End with at most three suggestions the user can act on (top up a budget, check a declined ad,
  look at an ad with no views). Do not change anything; offer to do it.
