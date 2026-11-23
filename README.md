# uptime

Scheduled health checks for Laventia Hub endpoints.

Runs every 10 minutes via GitHub Actions (`*/10 * * * *`) and checks:

- `/healthz` on the main site — expects `200`
- the tarot subdomain root — expects `401` (auth-gated)
- the card subdomain `robots.txt` — expects `200`

Each check retries once (2 attempts, 20s apart) before being treated as a failure.
On failure, it posts a short Thai alert to a Discord webhook configured via the
`DISCORD_WEBHOOK_URL` repository secret. If the secret is empty, the notification
step is skipped — the workflow still fails (so the Actions tab shows red) but
doesn't error out.

Trigger manually from the Actions tab (`workflow_dispatch`) to test connectivity
or verify the Discord alert path.
