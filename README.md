# TG Ads Manager for Claude

Manage your Telegram Ads from a conversation with Claude: see how your ads are doing, create ads, start and
stop them, change CPM and daily limits, and move money between the cabinet balance and ad budgets.

This repository is a Claude plugin marketplace with one plugin, `tg-ads-manager`. The plugin contains:

- the **TG Ads Manager connector** (`https://mcp.tgadsmanager.uz/mcp`), which you sign in to with your
  TG Ads Manager account;
- six **skills** that teach Claude the everyday work: a daily check, creating an ad safely, changing running
  ads, ad budgets, changing many ads at once, and general rules.

You need a TG Ads Manager account with at least one connected Telegram Ads cabinet: https://tgadsmanager.uz

## Two ways to connect

1. **This plugin** (recommended): the connector plus the skills.
2. **Connector only**: add `https://mcp.tgadsmanager.uz/mcp` as a custom connector in your AI app.
   Everything works, but without the skills Claude has to work out the steps by itself.

## Install

### claude.ai and the Claude desktop app

1. Open **Customize → Plugins → Add → Add marketplace**.
2. Enter the repository: `bilolkobilov/tg-ads-manager-claude`
3. Open **TG Ads Manager** in the list and select **Add**.
4. On the plugin's **Connectors** tab, add and connect the TG Ads Manager connector and sign in.
5. Start a chat and ask, for example, "How are my ads doing today?"

Connector only: **Customize → Connectors → Add custom connector**, name `TG Ads Manager`,
address `https://mcp.tgadsmanager.uz/mcp`.

### Claude Code

```text
/plugin marketplace add bilolkobilov/tg-ads-manager-claude
/plugin install tg-ads-manager@tg-ads-manager
```

Then run `/mcp`, select `tg-ads-manager` and sign in in the browser.

### ChatGPT

ChatGPT has no plugins of this kind. Add `https://mcp.tgadsmanager.uz/mcp` as a custom connector in
ChatGPT's settings, then **select the connector in the chat before you ask** for the task.

## Permissions

When you connect, TG Ads Manager asks what the AI app may do:

- **View only** — the AI can read your cabinets, ads and statistics. It cannot change anything.
- **View and manage** — the AI can also create and change ads and move money between the cabinet balance
  and ad budgets. Claude asks you before each change.

Every change goes to your real Telegram Ads cabinet. Telegram reviews every new ad, and editing the text,
link or targeting of an active ad sends it back to review.

## Disconnect

On https://tgadsmanager.uz open **Settings → Connected AI apps** and disconnect the app. Access stops at once.
You can also remove the plugin in **Customize → Plugins** (or `/plugin uninstall tg-ads-manager@tg-ads-manager`
in Claude Code).

---

## O'zbekcha

Claude bilan suhbatda Telegram reklamalaringizni boshqaring: natijalarni ko'rish, reklama ochish, to'xtatish va
yoqish, CPM va kunlik limitni o'zgartirish, kabinet balansi va reklama byudjeti o'rtasida pul o'tkazish.
Kerak: https://tgadsmanager.uz da akkaunt va kamida bitta ulangan Telegram Ads kabineti.

**Ulashning ikki yo'li:** (1) shu plagin — connector va ko'nikmalar (skills); (2) faqat connector —
`https://mcp.tgadsmanager.uz/mcp` manzilini AI ilovada custom connector sifatida qo'shish.

**claude.ai va Claude desktop:** Customize → Plugins → Add → Add marketplace → repository: `bilolkobilov/tg-ads-manager-claude`
→ TG Ads Manager → Add → plaginning Connectors bo'limida connectorni ulang va kiring.

**Claude Code:** `/plugin marketplace add bilolkobilov/tg-ads-manager-claude`, keyin `/plugin install tg-ads-manager@tg-ads-manager`,
keyin `/mcp` orqali kiring.

**ChatGPT:** bunday plaginlar yo'q. Manzilni custom connector sifatida qo'shing va vazifadan oldin chatda
connectorni tanlang.

**Ruxsat:** ulanishda tanlaysiz — **Faqat ko'rish** (AI faqat o'qiydi) yoki **Ko'rish va boshqarish** (AI
reklama ochadi, o'zgartiradi va kabinet balansi bilan reklama byudjeti o'rtasida pul o'tkazadi; har
o'zgarishdan oldin sizdan so'raydi).

**Uzish:** tgadsmanager.uz → **Sozlamalar → Ulangan AI ilovalar**.

## Русский

Управляйте рекламой в Telegram в диалоге с Claude: статистика, создание объявлений, запуск и остановка,
CPM и дневной лимит, перевод денег между балансом кабинета и бюджетом объявления.
Нужен аккаунт на https://tgadsmanager.uz и хотя бы один подключённый кабинет Telegram Ads.

**Два способа подключения:** (1) этот плагин — коннектор и навыки (skills); (2) только коннектор —
добавьте адрес `https://mcp.tgadsmanager.uz/mcp` как пользовательский коннектор (custom connector).

**claude.ai и Claude desktop:** Customize → Plugins → Add → Add marketplace → репозиторий: `bilolkobilov/tg-ads-manager-claude`
→ TG Ads Manager → Add → на вкладке Connectors плагина подключите коннектор и войдите.

**Claude Code:** `/plugin marketplace add bilolkobilov/tg-ads-manager-claude`, затем `/plugin install tg-ads-manager@tg-ads-manager`,
затем войдите через `/mcp`.

**ChatGPT:** таких плагинов нет. Добавьте адрес как пользовательский коннектор и перед задачей выберите
коннектор в чате.

**Доступ:** при подключении вы выбираете **Только просмотр** (ИИ только читает) или **Просмотр и управление**
(ИИ создаёт и меняет объявления и переводит деньги между балансом кабинета и бюджетами объявлений; перед
каждым изменением спрашивает вас).

**Отключение:** tgadsmanager.uz → **Настройки → Подключённые ИИ-приложения**.

## License

MIT — see [LICENSE](LICENSE).
