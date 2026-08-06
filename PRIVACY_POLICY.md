# Privacy Policy for LTC Assistant

Last Updated: 6 August 2026

This Privacy Policy explains how LTC Assistant ("the Bot", "we", "us") collects, uses, stores, and protects your information. LTC Assistant is built around strict privacy-first principles, using anonymised data storage, least-privilege permissions, and minimal data retention.

By using the Bot, you agree to the collection and processing of information in accordance with this policy.

## 1. Core Privacy & Security Principles

### Least-Privilege Intent Access
The Bot operates with Discord's `message_content` intent explicitly disabled. It cannot read general channel chat, user messages, or server chat history. The Bot only processes data when you directly invoke a slash command.

### Anonymised Data Storage
Raw Discord User IDs are not stored directly on disk for features like streaks, badges, or reminders. Stored user data is keyed using cryptographically hashed IDs (SHA-256 combined with a secure salt).

## 2. Information We Collect and Store

We only collect and store data necessary to provide and maintain the Bot's features. All persistent data is securely written to local storage using restricted file permissions (`0o600`) so only the bot process can access it.

* **Reminders (`/reminder`)**: We store your anonymised user key, the reminder text, the target user ID for delivery, a unique reminder ID, and the scheduled delivery time in UTC.
* **Daily Streaks & Badges (`/daily`, `/profile`, `/badges`)**: We store your anonymised user key, your current check-in streak, best check-in streak, last check-in date, and earned badge progress.
* **Daily Word Puzzle (`/wordquiz`)**: We store your anonymised user key, daily puzzle guess history, completion status, win count, and current win streak.
* **Extended Quality & Diagnostic Monitoring (`/connectpeople`)**: For ongoing quality assurance, bug analysis, and command logic verification, temporary interaction data (including submitted person names, anonymised user keys, user IDs, model version used, execution duration, and diagnostic status) is recorded to local storage (`connectpeople_monitor.json`). This diagnostic logging is temporary and strictly used for bug auditing and feature optimization.
* **Service Disclaimer Records**: We store your anonymised user key alongside the timestamp of when you accepted the first-time service disclaimer.
* **Server Welcome Settings (`/setwelcome`)**: When an administrator configures welcome messages, we store the Discord Server ID, selected Welcome Channel ID, and custom message template text.

## 3. Temporary & In-Memory Data Processing

Certain features rely on temporary in-memory (RAM) processing to function safely without persisting your inputs to disk.

* **Conversation Memory (`/ask`)**: When you use `/ask`, your question and recent conversation context are held temporarily in RAM for up to 15 minutes to enable follow-up replies. Discord response messages automatically self-delete after 15 minutes.
* **Instant Session Purge ("Panic Burn")**: Clicking the Delete button on any `/ask` response immediately flushes the active session from RAM and deletes the message from Discord.
* **Rate-Limit Quotas**: Daily usage limits (up to 30 queries per day) are tracked using temporary timestamps stored in RAM that clear after 24 hours. These quotas are never written to disk.

## 4. Third-Party Services & API Processing

To provide specific features, the Bot routes queries to external service providers. We do not sell or share your personal data with any third parties beyond these essential service connections.

* **Google Gemini API**: When you use `/ask` or `/connectpeople`, your input text is transmitted to Google's Gemini API (`gemini-3.6-flash` and fallback models) to generate a response. Queries sent to Google are subject to Google's Privacy Policy. We do not save your `/ask` prompts to permanent files.
* **Roblox Public APIs**: When you look up a profile via `/robloxuser`, the Bot queries official public Roblox endpoints (`roblox.com`, `users.roblox.com`, `presence.roblox.com`, `thumbnails.roblox.com`, and `groups.roblox.com`) to retrieve public profiles, avatars, and group lists. We do not store Roblox lookup history or user data locally.

## 5. How We Use Your Information

We use the collected information strictly to:
* Maintain your active reminders and deliver timely Direct Message notifications.
* Track and display check-in streaks, WordQuiz results, and profile badges.
* Send automated welcome messages in servers where administrators have enabled the feature.
* Generate responses and biographical connection chains upon request.
* Conduct temporary diagnostic monitoring for `/connectpeople` logic verification and bug analysis.
* Enforce fair-use limits on processing.

## 6. Your Data Rights & Self-Service Controls

We respect your rights under privacy legislation (including the UK GDPR). We grant all users direct control over their data.

* **Right to Access & Inspection**: You can view your stored profile badges, streaks, and active reminders at any time using `/profile` and `/reminder`.
* **Self-Service Erasure (`/privacy`)**: You can permanently wipe all your personal data from the Bot's database at any time. Run `/privacy`, choose **Delete Stored Data**, and confirm. This permanently deletes your reminders, streaks, badges, WordQuiz records, disclaimer history, and diagnostic telemetry logs, while instantly purging any active sessions from RAM.
* **DM Cleanup Tool**: You can use the **Clear DM Messages** button within the `/privacy` menu inside Direct Messages to automatically remove previous Bot messages from your chat log.

## 7. Changes to This Privacy Policy

We may update this Privacy Policy from time to time to reflect bot updates or legal requirements. Updated versions will be indicated by the "Last Updated" date above.

## 8. Contact Information

If you have questions regarding this Privacy Policy or need help exercising your data privacy rights, please contact the bot owner directly on Discord: `ltchaotic` (`<@363601406445355008>`).
