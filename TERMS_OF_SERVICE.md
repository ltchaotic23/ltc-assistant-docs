# Terms of Service for LTC Assistant

Last Updated: 6 August 2026

Welcome to LTC Assistant. These Terms of Service ("Terms") govern your access to and use of the LTC Assistant Discord Bot ("the Bot", "the Service"). Please read them carefully.

By adding the Bot to a Discord server, interacting with its slash commands, or using it within Direct Messages or User-Installed App contexts, you confirm that you have read, understood, and agreed to be bound by these Terms. If you do not agree, you must not use the Service.

---

## 1. Description of the Service

LTC Assistant is a multi-purpose Discord utility bot developed and operated by **ltchaotic**. It is designed with a privacy-first, least-privilege security model: Discord's `message_content` intent is explicitly disabled, meaning the Bot can never read general channel messages or server chat history. The Bot operates solely on data you explicitly provide through slash command interactions.

The Service includes, but is not limited to, the following features:

- **AI Assistant (`/ask`)**: Submit questions for an AI-generated response with optional 15-minute multi-turn conversation memory. Responses are private by default and auto-delete after 15 minutes.
- **People Connection Finder (`/connectpeople`)**: Submit two names to receive an AI-generated shortest historical or biographical connection chain between them, subject to a daily usage quota.
- **Personal Reminders (`/reminder`)**: A self-service step-by-step reminder management centre, allowing you to create, view, edit, and delete up to 50 active personal reminders.
- **Daily Check-In Streaks & Badges (`/daily`, `/profile`)**: A daily check-in system that tracks streaks and awards tiered achievement badges (Bronze through Diamond) across three badge categories.
- **Daily Word Puzzle (`/wordquiz`)**: A 5-letter daily Wordle-style word challenge with up to 6 attempts, with streak and win tracking.
- **Roblox User Lookups (`/robloxuser`)**: Retrieves publicly available profile information, avatar images, presence status, social statistics, and group memberships from Roblox's public APIs.
- **Server & User Information (`/serverinfo`, `/userinfo`, `/about`, `/help`)**: Informational displays of Discord server and user profile data. No data from these commands is stored.
- **Server Welcome Onboarding (`/setwelcome`)**: Administrator-configurable automated welcome message system for Discord servers.
- **Privacy & Data Management (`/privacy`)**: Self-service tools to review data handling, permanently delete all stored personal data, and clean up Direct Message history.

---

## 2. Eligibility & Age Requirement

In compliance with Discord's Terms of Service, you must be at least 13 years of age, or the minimum age of digital consent applicable in your jurisdiction, to use the Service. By using the Service, you represent and warrant that you meet this requirement.

---

## 3. Acceptable Use & User Conduct

By using the Service, you agree **not** to:

- **Attempt to bypass rate limits or quotas**: The Service enforces a 30-query daily limit across `/ask` and `/connectpeople`, a 15-second per-command cooldown on `/ask` and `/connectpeople`, and a 3-second cooldown on `/wordquiz`. You must not attempt to circumvent these limits through any means.
- **Abuse or overload the Service**: You must not deliberately send requests designed to crash, overload, or degrade the performance of the Bot or its underlying infrastructure.
- **Reverse-engineer or exploit the Service**: You must not attempt to reverse-engineer, decompile, or exploit any aspect of the Bot, its code, its API integrations, or the server infrastructure.
- **Submit harmful or unlawful content**: You must not use `/ask`, `/reminder`, welcome message templates, or any other input field to generate, store, or distribute content that is illegal, harmful, harassing, hateful, or in violation of Discord's Terms of Service or Community Guidelines.
- **Attempt prompt injection or security attacks**: You must not embed instructions within person names, reminder text, or questions that attempt to manipulate the Bot's AI behaviour, bypass safety filters, or extract system configuration.
- **Misuse personal data of others**: You must not use the Bot's lookup features to facilitate stalking, harassment, or any form of targeted harm against other individuals.
- **Exceed storage quotas**: You may maintain a maximum of 50 active reminders at any one time.

---

## 4. Third-Party Services & Integrations

Certain features of the Service depend on third-party APIs. By using these features, you acknowledge that your data will be processed by these third parties in accordance with their respective policies.

- **Google Gemini API** (`/ask`, `/connectpeople`): Your input text is transmitted to Google's Gemini AI API over an encrypted connection to generate responses. Use of these commands constitutes consent to that transmission. Google's processing is governed by [Google's Privacy Policy](https://policies.google.com/privacy).
- **Roblox APIs** (`/robloxuser`): Profile lookups query publicly available endpoints on Roblox's official API infrastructure. Only publicly accessible data is retrieved. No authentication credentials belonging to the queried user are accessed.

We do not sell your data or share it with third parties outside of these functional integrations.

---

## 5. AI Feature Terms & Disclaimer

The following additional terms apply to AI-powered features (`/ask`, `/connectpeople`):

- **First-Time Disclaimer**: Before using `/ask` for the first time, you must accept an in-app service disclaimer. This acceptance is recorded using your pseudonymised user key and may be revoked at any time by deleting your data via `/privacy`.
- **No Sensitive Input**: You must not submit secrets, passwords, confidential personal data, financial information, or sensitive third-party data as part of any AI query.
- **Session Lifespan**: Conversation memory for `/ask` exists in RAM for up to 15 minutes following the most recent reply. The Discord response message is automatically deleted after 15 minutes. You may also immediately delete a session using the **Delete** button.
- **Character Limits**: `/ask` questions are limited to 1,000 characters. `/connectpeople` person name inputs are limited to 80 characters each after sanitisation.
- **Accuracy & Reliability**: AI-generated responses are provided for informational and general-assistance purposes only. Outputs may contain inaccuracies, omissions, or be subject to safety filter restrictions. You must not rely on responses for professional, medical, legal, financial, or safety-critical advice.
- **Safety Filters**: Content that triggers Google's Gemini safety or content moderation filters will not be delivered. The Bot will notify you if a request is blocked for this reason.

---

## 6. Data Practices Summary

The Bot's full data collection and retention practices are documented in the accompanying [Privacy Policy](https://ltchaotic23.github.io/ltc-assistant-docs/PRIVACY_POLICY.md). Key points:

- User data is stored using pseudonymised keys (SHA-256 + server-side salt); raw Discord User IDs are not used as storage keys for personal data files, with the limited exception of reminder delivery references and diagnostic telemetry entries (used solely to enable delivery and support erasure requests).
- All persistent data files use restricted OS-level permissions and atomic write operations.
- AI usage quotas and conversation memory are held in RAM only and are never written to disk.
- Users may permanently delete all stored data at any time via `/privacy`.

---

## 7. Intellectual Property

The Bot, its code, commands, and associated documentation are the intellectual property of the developer (**ltchaotic**). No part of the Service may be reproduced, distributed, or used to create derivative works without explicit written permission.

---

## 8. Service Availability & Modifications

The Service is provided on a best-effort basis. We make no guarantees regarding uptime, continuous availability, or the preservation of data in the event of server failure or discontinuation. We reserve the right to:

- Modify, suspend, or discontinue any feature or the Service as a whole at any time, with or without notice.
- Update these Terms at any time; continued use of the Service constitutes acceptance of updated Terms.
- Remove, restrict, or ban any user or server from accessing the Service at our sole discretion, without prior notice, where conduct violates these Terms, disrupts the Service, or abuses Bot resources.

---

## 9. Disclaimer of Warranties & Limitation of Liability

- **"As Is" Service**: The Service is provided on an "as is" and "as available" basis. We make no warranties, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, or uninterrupted availability.
- **Limitation of Liability**: To the fullest extent permitted by applicable law, the owner and developer of LTC Assistant shall not be liable for any direct, indirect, incidental, special, consequential, or punitive damages arising from your use of, or inability to use, the Service, including but not limited to data loss, automated delivery delays, or inaccurate AI-generated content.

---

## 10. Governing Law

These Terms shall be governed by and construed in accordance with the laws of England and Wales. Any disputes arising under or in connection with these Terms shall be subject to the exclusive jurisdiction of the courts of England and Wales.

---

## 11. Contact

If you have questions, concerns, or requests regarding these Terms, please contact the bot owner directly on Discord: **ltchaotic** (`<@363601406445355008>`).
