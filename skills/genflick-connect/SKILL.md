---
name: genflick-connect
description: Create a Genflick account or sign in and connect an assistant using the user's email address, an expiring email link and the host's supported authentication flow.
---

Read the current onboarding guidance at `https://genflick.com/agents.txt`. Use the sign-in options actually offered by the deployment; source or packaging work does not establish that a new authentication method is live.

Start the host's Genflick connection flow and keep its callback and selected account. On the Genflick sign-in page, choose **Continue with email** and provide the user's chosen email address. The same flow handles existing and new accounts. The email request creates an unverified account when needed; consuming the link verifies mailbox ownership and signs into that account. Do not require a Google session or create a password to get started.

When the agent already has an authorized email connection for that mailbox, retrieve the sign-in message for this request, match the recipient and time, and open its link through the connection flow. Use the user's existing mailbox tools; do not ask for their email password or read another application's credential store. Otherwise let the user open the emailed link. The link works once and expires after ten minutes; request a fresh one if it expired or was consumed. Keep sign-in links and tokens out of chat, logs and saved project files.

On first email-link use, the dashboard may offer an optional password and confirmation. Close it, click outside it or continue without one unless the user asked to set it. The account remembers dismissal. Preserve the original workspace, WhatsApp continuation, homepage draft or assistant connection destination throughout sign-in.

Finish OAuth through the host so it stores its own access and refresh tokens. Never use a website-session cookie as an MCP token. Confirm success with authenticated tool discovery or an available profile read; mail delivery alone does not complete the connection. Use the account's existing permissions and spending settings for later work.

On Hermes v0.23.1, this package needs the native OAuth connection described in its README and `config.example.yaml`. That configuration intentionally takes precedence over the portable server entry and retains `trust: untrusted`. Do not claim standalone one-click OAuth or use device-code login unless the deployed Genflick issuer advertises and supports that grant.

For WhatsApp-first onboarding, Genny can ask the sender for an email and include a private connection link in the same message. An exact email reply starts the shared email-link request; opening the emailed link verifies the mailbox before the number is linked. Original creative messages are retained, while the email reply is excluded from creative intake. Automatic connections grant no paid spending or proactive notification opt-in. Existing-number replacements retain a review step.
