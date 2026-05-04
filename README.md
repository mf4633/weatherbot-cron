# weatherbot-cron

External cron driver for [weatherbot-mf.netlify.app](https://weatherbot-mf.netlify.app). Public repo with only workflow YAML so the main weatherbot codebase can stay private while still getting unlimited free GitHub Actions minutes for the `*/5 * * * *` schedules.

Two jobs, both fire every 5 minutes via GitHub Actions cron:

- `trader-cron.yml` → hits `/api/jackson_trader` (real-money bot)
- `paper-cron.yml` → hits `/api/paper_logger` (paper-trading bookkeeper + residual logger)

Auth: HTTP Basic via the `WEATHERBOT_BASIC_AUTH` repo secret (format `user:password`).
