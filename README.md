# weatherbot-cron

External cron driver for [weatherbot-mf.netlify.app](https://weatherbot-mf.netlify.app). Public repo with only workflow YAML so the main weatherbot codebase can stay private while still getting unlimited free GitHub Actions minutes for the `*/5 * * * *` schedules.

Jobs (all fire via GitHub Actions cron):

- `trader-cron.yml` (*/5) → hits `/api/jackson_trader` (real-money bot)
- `paper-cron.yml` (*/5) → hits `/api/paper_logger` (paper-trading bookkeeper + residual logger)
- `calibration-cron.yml` (*/15) → triggers `/api/calibration_update` (σ-calibration background fn)
- `data-logger-cron.yml` (hourly) → records the Kalshi book + obs (`/api/market_logger`) and drives the Claude verification scoreboard (`/.netlify/functions/claude_log-background` predict+settle, then reads back `?mode=status` / `?mode=latest` for visibility)

Auth: HTTP Basic via the `WEATHERBOT_BASIC_AUTH` repo secret (format `user:password`).

