---
name: change-running-ad
description: Change an existing Telegram ad in TG Ads Manager — start or stop it, raise or lower its CPM, set or remove its daily limit, or edit its text, link, button, media or targeting. Use when the user says pause, resume, stop, start, change the bid or CPM, limit daily spend, fix the text, e.g. "reklamani to'xtat", "подними CPM", "change the link".
---

# Change a running ad

Pick the smallest tool for the change. Each one changes the real ad on Telegram.

## Which tool

| The user wants to... | Tool | Goes back to Telegram review? |
|---|---|---|
| Start or stop the ad | `set_ad_status` (`active: true` / `false`) | No |
| Change the CPM (bid per 1000 views) | `set_ad_cpm` (`cpm`) | No |
| Set the daily limit, or `"0"` to remove it | `set_daily_budget` (`dailyBudget`) | No |
| Change text, link, button, media, targeting, schedule | `edit_ad` (the whole `form`) | Yes, if the ad is active |
| Add or return budget | see the `ad-budget-money` skill | No |

Never use `edit_ad` only to change CPM or the daily limit. `edit_ad` never changes the budget.

## Steps

1. Find the ad: `list_cabinets` if needed, then `list_ads` with `cabinetId` (use `search` with
   part of the title). Confirm the exact ad when more than one matches.
2. Read it: `get_ad` with `adId` shows status, CPM, budget left, daily limit, text, link and targeting.
3. Optional for CPM: `get_price_advice` with `cabinetId` returns, for active ads, a suggested CPM
   when there is one. Show it as a figure; the user decides.
4. Say the change in one line, old value → new value, with the currency, and get a yes.
5. Call the tool with `cabinetId`, `adId` and the new value. Amounts are text with a dot, e.g. `"1.5"`.

## Editing text, link or targeting

1. Call `get_ad_form_rules` with `cabinetId` first.
2. Build the full form from `get_ad` and change only what the user asked.
3. Call `check_ad` for the new text and link; when targeting channels or bots by name, call
   `check_targets` and drop the names Telegram refuses (tell the user which).
4. Before saving an active ad, tell the user: saving sends the ad back to Telegram review, and it
   may not show until Telegram approves it. Get a yes, then call `edit_ad`.
5. The target type of an existing ad (channels, bots, users, search) cannot be changed. For a new
   target type, create a new ad (use `create_similar_ad`, then the `create-telegram-ad` skill).

## After the call

- "Done" — report the new value.
- Refused — show Telegram's words.
- Still being sent — say so and stop; do not send it again.
- "Same request, not sent again" — ask the user whether they want it done a second time; only on
  a yes call the same tool again with `sendAgain: true`.
- To see what changed and who made it, use `get_ad_changes`.
