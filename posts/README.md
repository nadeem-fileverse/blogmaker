# ddocs-github-app

GitHub App that auto-deploys static blogs/docs to IPFS via Pinata. When you push to a connected repository, the app receives a webhook, builds the site content, pins it to IPFS through Pinata, and tracks deployment versions in MongoDB.

## Tech Stack

- **Runtime:** Node.js, TypeScript (ESM)
- **Framework:** Express
- **Database:** MongoDB (Mongoose)
- **GitHub Integration:** Octokit (`@octokit/app`)
- **IPFS Pinning:** Pinata SDK
- **Logging:** Pino
- **Validation:** Zod

## Prerequisites

- Node.js 18+
- MongoDB (local or remote)
- [Pinata](https://pinata.cloud) account (JWT + gateway domain)
- A registered [GitHub App](https://docs.github.com/en/apps/creating-github-apps) with webhook permissions
- [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) (for local testing)

## Getting Started

```bash
git clone <repo-url>
cd ddocs-github-app
npm install
```

Copy the example env file and fill in your values:

```bash
cp .env.example .env
```

### Environment Variables

| Variable | Description | Default |
|---|---|---|
| `GITHUB_APP_ID` | Your GitHub App's ID | — |
| `GITHUB_APP_PRIVATE_KEY` | PEM private key for the GitHub App | — |
| `GITHUB_WEBHOOK_SECRET` | Secret used to verify webhook payloads | — |
| `GITHUB_CLIENT_ID` | OAuth client ID of the GitHub App | — |
| `GITHUB_CLIENT_SECRET` | OAuth client secret of the GitHub App | — |
| `PINATA_JWT` | Pinata API JWT token | — |
| `PINATA_GATEWAY_DOMAIN` | Your Pinata gateway domain | — |
| `MONGO_URI` | MongoDB connection string | `mongodb://localhost:27017` |
| `DB_NAME` | Database name | `ddocs-github-app` |
| `PORT` | Server port | `3000` |
| `LOG_LEVEL` | Pino log level | `debug` |
| `SERVER_URL` | Public-facing server URL | `http://localhost:3000` |
| `NODE_ENV` | Environment | `development` |

## Local Testing with Cloudflared Tunnel

GitHub delivers webhooks to a public URL, so local development requires a tunnel. [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) gives you a free, temporary public URL that forwards traffic to your local server.

1. **Install cloudflared**

   ```bash
   brew install cloudflared
   ```

2. **Start the tunnel**

   ```bash
   cloudflared tunnel --url http://localhost:3000
   ```

   cloudflared will print a URL like `https://random-words.trycloudflare.com` — copy it.

3. **Update your GitHub App webhook URL**

   Go to your GitHub App settings and set the webhook URL to:

   ```
   https://<tunnel-url>/api/github/webhooks
   ```

4. **Update `.env`**

   Set `SERVER_URL` to your tunnel URL:

   ```
   SERVER_URL=https://<tunnel-url>
   ```

5. **Start the dev server**

   ```bash
   npm run dev
   ```

6. **Trigger a test event**

   Push a commit to a repository that has the GitHub App installed. You should see the webhook arrive in your server logs and the deployment flow kick off.

> **Note:** The tunnel URL changes every time you restart cloudflared. Remember to update both the GitHub App webhook URL and `SERVER_URL` in `.env` each time.

## API Endpoints

| Method | Path | Description |
|---|---|---|
| `GET` | `/api/health` | Health check |
| `POST` | `/api/upload` | Upload a tarball for IPFS pinning (signature-verified) |
| `GET` | `/api/versions/:owner/:repo` | List deployment versions for a repo |
| `GET` | `/api/versions/:owner/:repo/latest` | Get the latest deployment version |
| — | `/api/github/webhooks` | GitHub webhook receiver (handled by Octokit middleware) |

## Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start dev server with hot reload (tsx watch) |
| `npm run build` | Build for production (tsup) |
| `npm start` | Run production build |
| `npm run typecheck` | Type-check without emitting |
| `npm run lint` | Lint with ESLint |
| `npm run lint:fix` | Lint and auto-fix |
| `npm run format` | Format with Prettier |
| `npm run format:check` | Check formatting |
