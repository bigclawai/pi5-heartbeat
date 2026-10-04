# pi5-heartbeat

Dead-man's switch for BigClaw's Pi5 agent server (see `PLAYBOOK.md` §10 in bigclaw-ai).

- Every 5 minutes, the Pi force-pushes a one-commit `heartbeat` branch containing only a timestamp and `ok`/`degraded`.
- Every 10 minutes, the `watch` workflow checks how old that commit is. If the Pi has been silent for more than 20 minutes, or reports `degraded`, it messages the Chairman on Telegram.
- Repeat alerts go out hourly while the Pi stays down.

Nothing sensitive lives here. The Telegram credentials are encrypted repository secrets.
Manual test: Actions → watch → Run workflow → `test_alert: true`.
