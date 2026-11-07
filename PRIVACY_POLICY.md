# Privacy Policy for LTC Assistant

Last Updated: 7 November 2026

This policy explains what LTC Assistant ("the Bot") does with your information. The Bot is a free hobby project run by one developer, **ltchaotic** ("we", "us"). We try to keep as little about you as possible, and to keep what we do hold for no longer than we need it.

By using the Bot, you acknowledge this policy.

---

## In Short

- The Bot mostly works through slash commands. It only keeps what a feature needs: your reminders, your `/daily` streak and badges, whether you've accepted the `/ask` notice, and some `/connectpeople` diagnostics.
- Stored data is tied to a scrambled (pseudonymised) version of your Discord ID rather than your ID itself, except where a feature needs your real ID to work (for example, to DM you a reminder). Reminder contents are encrypted.
- `/ask` and `/connectpeople` send your question to Google's Gemini AI. Don't put anything sensitive in them.
- You can delete your stored data at any time with `/privacy`.

---

## 1. What We Store

The Bot keeps the following for as long as the feature needs it, or until you delete it:

- **Reminders (`/reminder`)**: the reminder text and when to send it, plus your Discord ID so the Bot can DM it to you. The text and your ID are encrypted. A reminder is removed once it's delivered or you delete it.
- **Streaks and badges (`/daily`, `/profile`)**: your check-in streak, your best streak, when you last checked in, and your badge progress.
- **`/ask` notice**: a record that you accepted the first-use notice, and when.
- **`/connectpeople` diagnostics**: for each use, the two names you entered, whether it worked, which AI model answered, how long it took, and any error. We use this to find bugs and check the AI's answers. Entries are kept for up to 60 days.
- **Server settings (`/serversetup`)**: if a server's admins set up welcome messages or auto-roles, the Bot stores the server's chosen channel, message and role. That's about the server, not about you. AutoMod rules are created in Discord itself; the Bot doesn't read or store the messages they check.

## 2. What We Don't Store

- **Your `/ask` conversations.** The Bot keeps your question and its answer in memory for up to about 15 minutes so you can ask follow-ups, then forgets them. The answer message is normally deleted automatically after about 15 minutes, and you can delete it straight away with the **Delete** button.
- **Usage limits.** To keep things fair, the Bot limits how often you can use the AI features. It counts your recent requests in memory only.
- **General chat.** The Bot doesn't read or keep normal chat messages, with the exceptions listed under "LTC Sandbox" below.
- **Lookups.** `/robloxinfo`, `/minecraftinfo`, `/discordinfo` and `/serverinfo` show public information when you ask for it. The results aren't saved.

## 3. LTC Sandbox and Other Servers We Run

Some features only run in servers the developer runs:

- **LTC Sandbox (Minecraft community server).** Messages in the game-chat channels are passed between Discord and the Minecraft server, showing your Discord name and your message. Server events (such as players joining, leaving or vouching for a friend, in-game bug reports, staff actions, and voice channel activity) are posted in the server's log channels. Playtime is shown on public leaderboards. To run the suggestions channel, the Bot also reacts to and opens threads on posts there.
- **Private servers we manage.** Some admin tools run only in the developer's own servers. For example, a tool there keeps members' roles in line with their linked Roblox group ranks. These tools may look up the Discord and linked public game-account details of members of those servers to do their job, and don't keep that information longer than they need it.

## 4. Services We Use

The Bot relies on other companies' services. Each has its own privacy policy:

- **Discord.** Everything you do with the Bot goes through Discord ([Discord Privacy Policy](https://discord.com/privacy)).
- **Google Gemini API** (`/ask`, `/connectpeople`). Your question is sent to Google to generate the answer ([Google Privacy Policy](https://policies.google.com/privacy), [Gemini API Terms](https://ai.google.dev/gemini-api/terms)). Some requests go through Google's free tier, where Google may use prompts and answers to improve its products and may have people review them. Others go through a paid tier, where Google says it doesn't use them for that. Either way, **don't enter passwords, secrets, financial details or other sensitive personal information.**
- **Public game APIs.** Lookups use public Roblox, Mojang/Minecraft and similar profile services (for example PlayerDB, mc-heads.net and crafthead.net) to fetch public profile information. The private-server tools above may also use Bloxlink to find which Roblox account a Discord member has linked.

We don't sell your data, and we only share it as needed to run these features. Some of these providers handle data outside the UK, including in the United States, under their own safeguards.

## 5. Keeping Data Safe

We take reasonable steps to protect what we store. For example, data is kept on a private server with restricted access, sensitive data is pseudonymised or encrypted, and stored files can only be read by the Bot. No system is perfectly secure, though, and we can't guarantee that data will never be lost or exposed.

The server also keeps short-lived technical logs (errors, which commands ran) so we can fix problems and spot abuse. These are deleted automatically, normally within about two weeks.

## 6. Why We Use Your Data (UK GDPR)

- **To provide the features you ask for** (reminders, streaks, AI answers): because it's needed to deliver the service you've chosen to use.
- **The `/ask` notice**: based on your agreement when you accept it.
- **Diagnostics, logs, server features and community features**: our legitimate interest, and the interest of server admins and communities, in running the Bot reliably, fixing bugs, preventing abuse and running their servers. We keep this to a minimum.

The Bot doesn't make automated decisions about you that have legal or similarly significant effects.

## 7. How Long We Keep It

| Data | Kept for |
| :--- | :--- |
| Reminders | Until delivered or deleted |
| Streaks, badges and the `/ask` notice | Until you delete your data, or the Bot shuts down |
| `/connectpeople` diagnostics | Up to 60 days |
| `/ask` conversations and usage limits | Memory only; gone within about a day at most |
| Server technical logs | Normally about two weeks |
| Data held by Google, Discord and others | Set by their own policies |

## 8. Your Rights and Controls

- **Delete your data**: `/privacy` → **Delete Stored Data** removes your reminders, streaks, badges, notice record and `/connectpeople` diagnostics, and clears any active `/ask` session.
- **Clean up DMs**: in DMs with the Bot, `/privacy` → **Clear DM Messages** removes the Bot's earlier messages.
- **See or change your data**: `/profile` shows your streaks and badges. `/reminder` lets you view, edit and delete reminders.

Under UK data protection law you can also ask to see, correct or delete your data, to limit or object to how we use it, or to get a copy of it. Contact us using the details below and we'll respond as soon as we reasonably can, within the time the law allows.

If you're unhappy with how we've handled your data, please tell us first so we can try to fix it. You can also complain to the UK Information Commissioner's Office: [ico.org.uk](https://ico.org.uk), helpline 0303 123 1113.

## 9. Age

You need to meet Discord's minimum age (at least 13, or older where your country requires it) to use the Bot.

## 10. Contact

LTC Assistant is run by **ltchaotic**, who is responsible for your data under UK data protection law.

- **Discord**: message **ltchaotic** (`<@363601406445355008>`)
- **Support server**: [discord.gg/Vm4y4pA3Yj](https://discord.gg/Vm4y4pA3Yj)
- **GitHub**: [ltc-assistant-docs issues](https://github.com/ltchaotic23/ltc-assistant-docs/issues)

## 11. Changes

We may update this policy as the Bot changes. The date at the top shows the latest version. If a change significantly affects how your data is used, we'll try to announce it in the support server.
