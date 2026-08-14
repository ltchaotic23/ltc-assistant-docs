# Privacy Policy for LTC Assistant

Last Updated: 14 August 2026

This Privacy Policy explains how LTC Assistant ("the Bot", "we", "us") collects, uses, stores, and protects your personal information. LTC Assistant is built around strict privacy-first principles, employing pseudonymised data storage, least-privilege Discord permissions, atomic file writes, and minimal data retention to protect user privacy at every layer.

By using the Bot, you agree to the collection and processing of information in accordance with this policy.

---

## 1. Core Privacy & Security Principles

### Least-Privilege Intent Access
The Bot operates with Discord's `message_content` intent explicitly disabled. This means the Bot cannot read general channel messages, server chat history, or any messages you send outside of a slash command. The `members` intent is enabled solely to resolve member objects when displaying server membership information in commands such as `/userinfo`, and is not used for any form of mass data collection.

### Pseudonymised Data Storage
Raw Discord User IDs are not stored directly on disk for any user-facing features (streaks, badges, reminders, puzzles, or disclaimer records). Instead, persistent data is keyed using a cryptographic pseudonym: a truncated SHA-256 hash of your Discord User ID combined with a private, server-side salt value. This means stored data cannot be attributed to a specific Discord account without access to both the original User ID and the private salt. Under the UK GDPR and EU GDPR, this is classified as pseudonymisation rather than full anonymisation, as the link to your identity can theoretically be re-established using the original identifier.

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

Check-ins are eligible once per 20-hour window (not strictly once per calendar day). Badge progress across three tiers — Greeter 👋, Timekeeper ⏰, and Historian 📜 — is also stored per badge, including progress count and the date of last increment.

### Daily Word Puzzle (`/wordquiz`)
- Your pseudonymised user key
- The date of your current puzzle attempt
- Your submitted guesses and their results for the current daily puzzle
- Your puzzle completion status and whether you solved it
- Your total wins and current win streak count
- Total games played count

### AI Service Disclaimer (`/ask` — First-Time Acceptance)
- Your pseudonymised user key
- The UTC ISO 8601 timestamp at which you accepted the first-time service disclaimer

### Server Welcome Configuration (`/setwelcome`)
- The Discord Server (Guild) ID of the server being configured
- The Discord Channel ID of the selected welcome channel
- The text of any custom welcome message template set by a server administrator

This data is set and managed exclusively by server administrators. No user-level personal data is collected by this feature.

### `/connectpeople` Diagnostic Telemetry
For ongoing quality assurance, bug analysis, and model performance verification, a structured log entry is recorded for each use of `/connectpeople`. Each entry contains:
- A short random internal record identifier
- The UTC timestamp of the request
- Your pseudonymised user key (or `activity_token`)
- The sanitised names of both people submitted
- The status of the request (e.g. success, error, or safety block)
- The AI model that generated the response (e.g. `claude-sonnet-5`, `gemini-3.6-flash`)
- The execution duration in seconds
- The length of the generated response in characters
- The degrees-of-separation figure extracted from the response (if any)
- Any error detail string (in the event of a failure)

Raw Discord User IDs are **not** recorded in telemetry entries. Entries are linked to you exclusively through your pseudonymised key. When you request erasure via `/privacy`, all telemetry entries matching your account are permanently removed. The telemetry log is capped at 50 entries per user on a rolling basis; oldest entries are automatically discarded when the cap is reached.

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

### Anthropic Claude API (Primary AI Engine)
When you use `/ask` or `/connectpeople`, your input query text is transmitted over an encrypted HTTPS connection to Anthropic's Messages API (`https://api.anthropic.com/v1/messages`). We use a paid Commercial API key (`claude-sonnet-5`), which operates under **Anthropic's Commercial Terms of Service**:

* **Zero Model Training**: Traffic sent through our paid API key falls under Anthropic's Commercial Terms. Your prompts and Claude's responses are **never used to train Anthropic's AI models**, full stop, regardless of any setting. This is an explicit contractual guarantee without any opt-in/opt-out toggles required.
* **30-Day Security & Abuse Retention**: Inputs and outputs are held on Anthropic's backend for a standard window of **30 days** purely for trust & safety, abuse detection, and legal compliance, after which they are automatically deleted.
* **Automated Safety Classifiers**: Anthropic runs automated safety classifiers over submitted content solely to screen for policy violations (such as CSAM, cyberattack tooling, or weapons instructions). This is strict abuse screening—Anthropic performs no behavioral analytics, advertising profiling, or user tracking on API traffic.

### Google Gemini API (Fallback AI Engine)
If the primary Claude model is temporarily unavailable, rate-limited, or experiencing latency, the Bot automatically routes the request through Google's Gemini AI API (`gemini-3.6-flash` ➔ `gemini-2.5-flash` ➔ `gemini-2.0-flash` ➔ `gemini-1.5-flash`). This transmission is governed by [Google's Privacy Policy](https://policies.google.com/privacy) and the [Gemini API Terms of Service](https://ai.google.dev/gemini-api/terms).

> **Important Privacy Notice**: While our primary Claude integration guarantees zero model training, you should **never** submit secrets, passwords, confidential personal data, financial information, or sensitive third-party data into `/ask` or `/connectpeople`. The first-time `/ask` disclaimer reminds users of this before first use.

### Roblox Public APIs
When you use `/robloxuser`, the Bot queries official public Roblox API endpoints (`users.roblox.com`, `thumbnails.roblox.com`, `presence.roblox.com`, `friends.roblox.com`, `groups.roblox.com`) to retrieve publicly available profile data, avatar images, presence status, and group memberships. No Roblox lookup history or results are stored locally.

---

## 6. How We Use Your Information

Your data is used exclusively to:
- Deliver active reminders to your Discord Direct Messages at the scheduled time.
- Track and display your check-in streaks, badge progress, and WordQuiz history.
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
| WordQuiz state | Until user data wiped via `/privacy` |
| Disclaimer acceptance | Until user data wiped via `/privacy` |
| `/connectpeople` telemetry | Rolling cap (max 50 entries per user); permanently deleted on user erasure request |
| `/ask` conversation memory | Up to 15 minutes in RAM; never persisted to disk |
| AI usage quotas | Up to 24 hours in RAM; never persisted to disk |
| Anthropic API retention | 30 days on Anthropic backend (abuse screening only; zero model training) |

---

## 8. Your Data Rights & Self-Service Controls

We respect your rights under the UK General Data Protection Regulation (UK GDPR). All users have direct, self-service control over their stored data:

- **Right to Access**: You can view your stored badge progress, check-in streaks, and active reminders at any time using `/profile` and `/reminder`.
- **Right to Erasure (`/privacy` → Delete Stored Data)**: You may permanently delete all data the Bot holds about you at any time. This action removes your reminders, streak history, badge progress, WordQuiz records, disclaimer acceptance, and all `/connectpeople` telemetry entries linked to your account. Any active AI session is simultaneously purged from RAM. **This action is irreversible.**
- **DM Message Cleanup (`/privacy` → Clear DM Messages)**: Within Direct Messages, you may use this tool to automatically remove previous Bot messages from your Direct Message chat log.

---

## 9. Changes to This Privacy Policy

We may update this Privacy Policy from time to time to reflect feature updates, changes in data practices, or legal requirements. The "Last Updated" date at the top of this document will reflect the date of the most recent revision. Continued use of the Bot after an update constitutes acceptance of the revised policy.

---

## 10. Contact

If you have questions about this Privacy Policy or wish to exercise your data privacy rights, please contact the bot owner directly on Discord: **ltchaotic** (`<@363601406445355008>`).
