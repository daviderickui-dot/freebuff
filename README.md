# freebuff

## 24/7 SSH Shell via GitHub Actions

This project includes a GitHub Actions workflow that gives you SSH access to a
terminal running 24/7 (cycling every 6 hours on GitHub-hosted runners).

### How to use

1. **Push this repo to GitHub** (if not already there):
   ```bash
   git add .
   git commit -m "Add 24/7 SSH shell workflow"
   git push
   ```

2. **Trigger a session** — Go to your repo on GitHub → **Actions** →
   **Freebuff SSH Shell (24/7)** → **Run workflow** → **Run workflow**.

3. **Find the SSH address** — In the workflow run, click the `ssh-shell` job and
   find the `Setup tmate SSH session` step. The tmate SSH connection string
   will appear in that step's logs — something like:
   ```
   ssh <random>@<host>.tmate.io
   ```

4. **Connect** — Open your terminal and paste the SSH command:
   ```bash
   ssh <random>@<host>.tmate.io
   ```
   You'll get a full bash shell on the GitHub Actions runner.

5. **It stays alive** — The workflow runs for 6 hours (the GitHub max). A cron
   schedule restarts it automatically every 6 hours, so you have near-continuous
   access.

### ⚠️ Important notes

- **GitHub ToS** — This uses GitHub Actions as a makeshift terminal, which is
  not its intended purpose. Use responsibly and don't abuse it.
- **6-hour cycle** — Each session runs up to 6 hours, then a new one starts.
  Every restart generates a **new SSH address** — check the logs again.
- **Public repos** — Anyone with access to your repo can see the SSH address
  in the Actions logs. Use a private repo or enable `limit-access-to-actor` (it
  is on by default in the workflow).
- **Ephemeral storage** — The runner's filesystem is wiped after each session.
  Nothing persists between runs.
