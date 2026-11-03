# Daily sales report bot (Telegram + serverless)

## Problem
At ITSchool CI I had to send a Word sales report to management every evening, listing activities, client contacts, amounts and next-day actions. Filling in the template by hand took time and was easy to forget.

## Solution
I write to a Telegram bot during the day:

- client lines such as `Name ; phone ; source ; yes/no ; amount ; status`;
- activities, picked from checkboxes;
- next-day actions.

In the evening, the `/envoyer` command runs a 3-step confirmation. The bot then fills the company's Word template (with a TOTAL row) and emails the report to management, with a manager in copy. A copy is saved in the Sent folder. A reminder arrives every working day if nothing has been sent.

## Stack
- Node.js. The Word template is filled with docxtemplater.
- Emails are sent over SMTP with Nodemailer. A copy is saved through IMAP.
- It is deployed on Vercel: a Telegram webhook protected by a secret header, plus a daily cron job for the reminder.
- Data is stored per day in a Neon Postgres database (JSONB).
- At first it ran on my PC. I moved it online so it works when the computer is off.

## Status
I have used it in production since 29 October 2026 to send my real daily reports. I built it with AI coding assistance (Claude Code). I wrote the specifications, tested every step and deployed it.

The code is private because it contains company data. A demo can be shown on request.
