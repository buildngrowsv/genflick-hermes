# Genflick for Hermes

Connect Hermes to Genflick's creative and business suite: films, series, music videos, ads, creative work and marketing, using the same saved workspaces as the Genflick app.

Genflick owns saved projects, media, durable work, permissions and spending. Hermes owns the conversation, tool approvals and connection credentials. Discover the account's actual tools before promising an operation. This connector does not establish talent hiring, payments, payouts or earnings capabilities.

## Install

With Hermes **v0.23.1 or later**, install the reviewed repository:

```sh
hermes plugins install https://github.com/buildngrowsv/genflick-hermes
```

Until the catalog entry is merged, use the repository URL rather than claiming that `hermes plugins install genflick` is available. You can also download the release ZIP, extract it into the intended Hermes home's `plugins/genflick/`, and run `hermes plugins enable genflick`.

## Connect your account

**Hermes v0.23.1 requires one native OAuth configuration step.** The portable `mcp.json` entry does not carry an OAuth auth method, and `hermes mcp login` reads native `mcp_servers` configuration. The portable package alone therefore does not complete sign-in.

Merge the reviewed [config.example.yaml](config.example.yaml) into the intended Hermes profile's `config.yaml`, preserving other servers. Inspect an existing `genflick` entry before changing it. The native entry intentionally takes precedence over the same-name portable entry and sets `trust: full`:

```yaml
mcp_servers:
  genflick:
    url: https://genflick.com/mcp/studios
    auth: oauth
    trust: full
```

**Upgrading from 0.1.0:** 0.1.0 set `trust: untrusted`, which made Hermes ask before almost every Genflick step. In your `config.yaml`, change the `genflick` entry's `trust: untrusted` to `trust: full`, then restart Hermes.

Then use Hermes's supported connection flow:

```sh
hermes mcp login genflick
hermes mcp test genflick
```

Genflick sign-in accepts your existing email address. The one-use emailed link expires in **10 minutes**; neither Google sign-in nor a password is required. If Hermes already has an authorized mailbox connection, it can retrieve that request's email and follow the sign-in link while preserving the OAuth callback. Otherwise open the message yourself. Keep tokens and sign-in URLs private. An optional password prompt can be closed or skipped; the account remembers dismissal.

Finish OAuth through Hermes so Hermes stores its own tokens. Never substitute website cookies, another app's credentials or a pasted bearer token. Do not advertise this as one-click portable OAuth or an MCP device-code grant.

## Start with saved work

Ask Hermes to connect to Genflick, read your profile and list your saved projects. Read a selected workspace before editing it. The included `genflick` skill explains capability discovery, revisions, durable work, saved results and spending authority; `genflick-connect` covers email links, OAuth and the WhatsApp front door.

The product also supports entering through the homepage or Genny on WhatsApp. For an unconnected WhatsApp number, Genny can request an email and offer a private connection link. Mailbox verification precedes number linking; replacement of an existing connection requires review. Current front-door guidance: [agents.txt](https://genflick.com/agents.txt), [llms.txt](https://genflick.com/llms.txt).

## Verification and limits

The isolated Hermes v0.23.1 setup passed official plugin validation, the security scanner and Plugin Doctor. Plugin plus native OAuth completed sign-in, cached reconnect, discovery of 65 remote tools, and successful `get_profile` and `list_projects` reads against production. Hosted email-link creation/sign-in, used-link rejection, returning sign-in and remembered optional-password dismissal were also exercised.

This evidence covers connection and saved-work reads. Creative generation, edits, cancellation/recovery, advertising activation, social publication, CRM delivery, recurring jobs and monetization are separate workflows; this release does not claim that every such operation was qualified in Hermes. The actual connected tools, permissions and accepted budget decide what is available.

## Security and network disclosure

This package contains manifests, two skills, an OAuth configuration example and documentation. It adds no executable, shell command, background process, telemetry, self-updater, static authorization header or credential store. Enabled MCP calls send the requested operation and task inputs to **https://genflick.com/mcp/studios**. Authorized workflows may use downstream providers under Genflick's existing permissions and budget controls. Hermes manages OAuth tokens; Genflick independently enforces resource access and spending. `trust: full` means Hermes does not ask before each Genflick tool. Genflick enforces approval on its side: the account's credit confirmation threshold (50 credits unless the owner changed it; above it the creator approves in Genflick), each session's finite credit ceiling, exact-post approval before publishing, separate advertising and CRM permissions, and Stop.

## License and support

[MIT](LICENSE) covers only this connector's files. Genflick's hosted service, backend, customer data and other repositories are outside this license; use of the hosted service remains subject to [Genflick's terms](https://genflick.com/account-access/terms-of-service) and [privacy policy](https://genflick.com/account-access/privacy-policy).

Support: support@genflick.com. [Hermes plugin guide](https://hermes-agent.nousresearch.com/docs/developer-guide/plugins), [MCP guide](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp).
