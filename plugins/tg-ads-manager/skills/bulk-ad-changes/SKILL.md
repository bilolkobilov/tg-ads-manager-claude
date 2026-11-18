---
name: bulk-ad-changes
description: Change many Telegram ads at once in TG Ads Manager — pause or start several ads, set the same CPM or daily limit on a group, top up or return budget across ads, or copy ads to another cabinet. Use when the user says "all", "every", "these ads", a campaign, or a list, e.g. "hamma reklamalarni to'xtat", "подними CPM всем активным", "copy these ads to my EUR cabinet".
---

# Many ads at once

Read first, show the plan, get one yes, then apply and report.

## 1. Read

1. `list_cabinets` if the cabinet is not clear.
2. `list_ads` with `cabinetId` (filters: `status`, `search`; it is paged — read every page you
   need). For a campaign, `list_campaigns` with `campaignId` gives its ad ids.
3. Keep only the ads the user meant. If the selection is unclear, show it and ask.

## 2. Plan

1. For pause, start, CPM, daily limit, add or return budget, or delete, call `plan_bulk_action`
   with `cabinetId`, `adIds`, `kind` (`pause`, `resume`, `cpm`, `dailyBudget`, `addBudget`,
   `returnBudget`, `delete`) and `amount` where needed. It changes nothing and returns, per ad, the
   value before and after or why it is skipped, plus the money moved and the balance after.
2. Show the plan as a table, with the currency on every amount:

| Ad | Now | After | Note |
|----|-----|-------|------|

   Add the totals: how many changes, money moved, balance after, and skipped ads with the reason.
3. Ask once: "Apply these N changes?" Wait for a clear yes. A change to the plan needs a new yes.

## 3. Apply

Apply one ad at a time with the single-ad tool for that change:
`set_ad_status`, `set_ad_cpm`, `set_daily_budget`, `add_ad_budget`, `return_ad_budget`, `delete_ad`.

- Use exactly the values from the agreed plan.
- If a tool says there were too many changes in a minute, pause, tell the user, and continue the
  remaining ads after a minute. Do not hammer the tool.
- For money moves, follow the `ad-budget-money` skill: never resend a repeat on your own.
- `delete_ad` cannot be undone — say so in the plan.
- Copying ads to another cabinet: `copy_ads_to_cabinet` with `targetCabinetId` and up to the
  allowed number of `adIds`. Copies are created stopped with no budget. If the currencies differ,
  give each ad's CPM in `cpms`. Re-send only the `notCopiedAdIds` after fixing what each row asks.

## 4. Report

One table: ad, result (done / refused / still being sent), Telegram's words when refused.
Then one line each: how many succeeded, how many Telegram refused, how many are still being sent.
Do not retry refused ads on your own; offer to look at them with the user.
