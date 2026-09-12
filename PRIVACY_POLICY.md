# Privacy Policy for LTC Assistant

Last Updated: 2 September 2026

This Privacy Policy explains how LTC Assistant ("the Bot", "we", "us") collects, uses, stores, and protects your personal information. LTC Assistant is built around strict privacy-first principles, employing pseudonymised data storage, least-privilege Discord permissions, atomic file writes, and minimal data retention to protect user privacy at every layer.

By using the Bot, you agree to the collection and processing of information in accordance with this policy.

---

## 1. Core Privacy & Security Principles

### Least-Privilege Intent Access
The Bot operates with Discord's `message_content` intent explicitly disabled for general usage. This means the Bot cannot read general channel messages, server chat history, or any messages you send outside of a slash command. The `members` intent is enabled solely to resolve member objects when displaying server membership information in `/discordinfo` and to deliver automated welcome greetings and auto-roles when enabled by server administrators. It is never used for mass data scraping or harvesting.

### Pseudonymised Data Storage
Raw Discord User IDs are not stored directly on disk for any user-facing features (streaks, badges, reminders, or disclaimer records). Instead, persistent data is keyed using a cryptographic pseudonym: a truncated SHA-256 hash of your Discord User ID combined with a private, server-side salt value. This means stored data cannot be attributed to a specific Discord account without access to both the original User ID and the private salt. Under the UK GDPR and EU GDPR, this is classified as pseudonymisation rather than full anonymisation, as the link to your identity can theoretically be re-established using the original identifier.

### Atomic File Writes & Restricted Permissions
All data files are written atomically using a write-to-temporary-file-then-replace strategy, ensuring that an interrupted or concurrent write cannot corrupt stored data. All data files are created with restricted OS-level file permissions (`0o600`), meaning only the bot process itself can read or write them.

---

## 2. Information We Collect and Store

We collect and retain only the minimum data necessary to provide and maintain each feature. The following describes exactly what is stored for each feature.

### Reminders (`/reminder`)
- Your pseudonymised user key
- The reminder message text (encrypted at rest using Fernet symmetric encryption)
- The scheduled delivery time (UTC ISO 8601 timestamp)
- Your raw Discord User ID (encrypted at rest inside each reminder entry as `creator` to allow Direct Message delivery)
- A unique internal reminder identifier (UUID hex)

> **Note**: Your raw Discord User ID is encrypted at rest and retained within reminder entries solely to enable the bot to deliver your reminder to your Discord Direct Messages. It is not used for any other purpose and is permanently removed when you delete reminders or wipe your data via `/privacy`.

### Daily Check-In Streaks & Badges (`/daily`, `/profile`)
- Your pseudonymised user key
- Your current check-in streak count
- Your all-time best check-in streak count
- The ISO 8601 timestamp of your most recent check-in

Check-ins are eligible once per 20-hour window (not strictly once per calendar day). Tiered badge progress across all achievement categories — Daily Streak 🔥, Timekeeper ⏰, and Historian 📜 — is also stored per badge, including progress count and the date of last increment.

### AI Service Disclaimer (`/ask` — First-Time Acceptance)
- Your pseudonymised user key
- The UTC ISO 8601 timestamp at which you accepted the first-time service disclaimer

### Server Administration (`/serversetup`, `/setwelcome`)
- **Server Welcome Configuration**: The Discord Server (Guild) ID, selected Welcome Channel ID, and custom welcome message template.
- **Auto-Role Configuration**: The Discord Role ID chosen by administrators to automatically assign to new human members upon joining.
- **AutoMod Protection**: LTC Assistant configures native AutoMod rules (phishing, invite link shield, mention spam, toxicity) directly on Discord's edge infrastructure via the Discord API. The Bot does not inspect or log server messages for AutoMod.

This data is configured and managed exclusively by server administrators to operate server management tools. No individual user-level personal data is collected by these features.

### `/connectpeople` Diagnostic Telemetry
For ongoing quality assurance, bug analysis, and model performance verification, a structured log entry is recorded for each use of `/connectpeople`. Each entry contains:
- A short random internal record identifier
- The UTC timestamp of the request
- Your pseudonymised user key (or `activity_token`)
- The sanitised names of both people submitted
- The status of the request (e.g. success, error, or safety block)
- The AI model that generated the response (e.g. `gemini-3.8-flash`, `gemini-3.7-flash`, `gemini-3.6-flash`)
- The execution duration in seconds
- The length of the generated response in characters
- The degrees-of-separation figure extracted from the response (if any)
- Any error detail string (in the event of a failure)

Raw Discord User IDs are **not** recorded in telemetry entries. Entries are linked to you exclusively through your pseudonymised key. When you request erasure via `/privacy`, all telemetry entries matching your account are permanently removed. The telemetry log is capped at 50 entries per user on a rolling basis with automatic 60-day global expiration; oldest entries are automatically discarded when the cap or expiration is reached.

---

## 3. Temporary & In-Memory Data Processing

The following data is processed exclusively in the server's RAM and is never written to disk.

### Conversation Memory (`/ask`)
When you use `/ask`, your question and the AI response are held temporarily in RAM for up to 15 minutes. Within this window, you may submit follow-up questions, with the bot retaining up to the last 4 conversational exchanges (8 messages) in memory at any given time to provide coherent multi-turn responses. After 15 minutes of inactivity from the last reply, the session is automatically purged from RAM and the Discord response message is automatically deleted.

### Instant Session Purge ("Delete" / "Panic Burn")
Clicking the **Delete** 🗑️ button on any `/ask` response immediately removes the active session from RAM and deletes the Discord message, with no delay.

### Daily AI Usage Quotas
To ensure fair use, a limit of 30 AI requests per user per 24-hour rolling period is enforced across `/ask` and `/connectpeople` combined. This quota is tracked using in-memory timestamps and is **never written to disk**. Quota data clears automatically after 24 hours without any persistent record.

### Interactive UI State
UI component state (button interactions, select menus, paginator state) is held in RAM for the duration of the component's timeout (typically 3 minutes) and is discarded thereafter.

---

## 4. Data-at-Rest Security

All persistent data files are stored on a private server with no public-facing network access other than the bot process itself. Security measures include:

- **Restricted File Permissions**: All data files are created with OS-level permissions (`0o600`), restricting read and write access to the bot process only.
- **Atomic Writes**: Data is written to a temporary file and then atomically replaced, preventing corruption from interrupted writes or concurrent access.
- **Field-Level Encryption**: Sensitive data such as reminder text and recipient creator IDs are encrypted at rest using AES-128 CBC / HMAC SHA-256 via Fernet keys derived from server salt.
- **Private Server Access**: The server is accessible only via SSH with key-based authentication; no password-based login is enabled.

---

## 5. Third-Party Services & External Data Processing

To provide specific features, the Bot communicates with external service providers over encrypted HTTPS connections. We do not sell or share your personal data with any third party beyond these essential functional connections.

### Google Gemini API (Primary AI Engine)
When you use `/ask` or `/connectpeople`, your input query text is transmitted over an encrypted HTTPS connection to Google's official Gemini AI API endpoints (`gemini-3.8-flash` with fallbacks to `gemini-3.7-flash`, `gemini-3.6-flash`, `gemini-3.5-flash`, `gemini-3.5-flash-lite`, `gemini-3.1-flash-lite`, and `gemini-3-flash-preview`). This transmission is governed by [Google's Privacy Policy](https://policies.google.com/privacy) and the [Google Gemini API Terms of Service](https://ai.google.dev/gemini-api/terms):

* **API Processing & Product Improvement**: Under Google's standard / free tier API terms, submitted prompt queries and model outputs may be processed by Google to provide, maintain, and improve Google products and services, and may be reviewed by trained human reviewers for quality and safety.
* **Abuse & Safety Screening**: Google applies automated safety classifiers to detect policy violations (such as CSAM, malicious tooling, or harmful content) and retains request logs for security and statutory compliance.
* **No Local Disk Logging**: The Bot itself does not log or persist your `/ask` questions or answers to local disk files.

> **Important Privacy Notice**: Because Google processes free-tier API queries under its standard terms, you should **never** submit secrets, passwords, financial information, confidential personal data, or sensitive third-party credentials into `/ask` or `/connectpeople`. The first-time `/ask` disclaimer reminds users of this requirement before first use.

### Roblox Public APIs
When you use `/robloxinfo`, the Bot queries official public Roblox API endpoints (`users.roblox.com`, `thumbnails.roblox.com`, `presence.roblox.com`, `friends.roblox.com`, `groups.roblox.com`) to retrieve publicly available profile data, avatar images, presence status, and group memberships. No Roblox lookup history or results are stored locally.

---

## 6. How We Use Your Information

Your data is used exclusively to:
- Deliver active reminders to your Discord Direct Messages at the scheduled time.
- Track and display your check-in streaks and badge progress.
- Send automated server welcome messages where an administrator has configured this feature.
- Generate AI-powered responses and biographical connection chains upon request.
- Record diagnostic telemetry for `/connectpeople` to support quality assurance and bug resolution.
- Enforce daily AI usage quotas to ensure fair access for all users.

---

## 7. Data Retention

| Data Type | Retention Period |
| :--- | :--- |
| Active reminders | Until delivered, manually deleted, or user data wiped |
| Check-in streaks & badges | Until user data wiped via `/privacy` |
| Disclaimer acceptance | Until user data wiped via `/privacy` |
| `/connectpeople` telemetry | 60 days maximum (rolling 50-entry cap per user); permanently deleted on user erasure request |
| `/ask` conversation memory | Up to 15 minutes in RAM; never persisted to disk |
| AI usage quotas | Up to 24 hours in RAM; never persisted to disk |
| Google Gemini API retention | Governed by Google's Privacy Policy & Gemini API Terms (retained by Google for service delivery and product improvement) |

---

## 8. Your Data Rights & Self-Service Controls

We respect your rights under the UK General Data Protection Regulation (UK GDPR). All users have direct, self-service control over their stored data:

- **Right to Access**: You can view your stored badge progress, check-in streaks, and active reminders at any time using `/profile` and `/reminder`.
- **Right to Erasure (`/privacy` → Delete Stored Data)**: You may permanently delete all data the Bot holds about you at any time. This action removes your reminders, streak history, badge progress, disclaimer acceptance, and all `/connectpeople` telemetry entries linked to your account. Any active AI session is simultaneously purged from RAM. **This action is irreversible.**
- **DM Message Cleanup (`/privacy` → Clear DM Messages)**: Within Direct Messages, you may use this tool to automatically remove previous Bot messages from your Direct Message chat log.

---

## 9. Changes to This Privacy Policy

We may update this Privacy Policy from time to time to reflect feature updates, changes in data practices, or legal requirements. The "Last Updated" date at the top of this document will reflect the date of the most recent revision. Continued use of the Bot after an update constitutes acceptance of the revised policy.

---

## 10. Contact

If you have questions about this Privacy Policy or wish to exercise your data privacy rights, please contact the bot owner directly on Discord: **ltchaotic** (`<@363601406445355008>`).


### 6.4. Minecraft & NameMC Lookup APIs (`/minecraftinfo`)
When you use `/minecraftinfo`, the Bot queries official public Mojang and PlayerDB endpoints (`api.mojang.com`, `sessionserver.mojang.com`, `playerdb.co`, `mc-heads.net`) to retrieve publicly available Minecraft profile data, UUIDs, skin textures, and 3D renders. Direct links are provided to NameMC profiles. No Minecraft lookup history or results are stored locally.
