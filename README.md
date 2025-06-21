# Slack Notify – GitHub Composite Action

Send clean, GitHub-style Slack notifications for deployment pipelines across environments (`dev`, `uat`, `prod`).

## ✅ Features

- Shows commit count, SHA, and message
- Links directly to commit
- Labels environment and status (start/success/failure)
- Works with any GitHub repo and webhook

## 📦 Inputs

| Name           | Description                                 | Required |
|----------------|---------------------------------------------|----------|
| `status`       | One of: `start`, `success`, `failure`       | ✅       |
| `service`      | Name of the service                         | ✅       |
| `environment`  | Environment label (`dev`, `uat`, `prod`)    | ✅       |
| `slack_webhook`| Slack Incoming Webhook URL                  | ✅       |

## 🧪 Example Usage

```yaml
- name: Notify Slack - Start
  uses: common-fi/github-slack-notify/.github/actions/slack-notify@main
  with:
    status: start
    service: Service.Name
    environment: dev
    slack_webhook: ${{ secrets.SLACK_WEBHOOK_URL }}

- name: Notify Slack - Success
  if: success()
  uses: common-fi/github-slack-notify/.github/actions/slack-notify@main
  with:
    status: success
    service: Service.Name
    environment: dev
    slack_webhook: ${{ secrets.SLACK_WEBHOOK_URL }}

- name: Notify Slack - Failure
  if: failure()
  uses: common-fi/github-slack-notify/.github/actions/slack-notify@main
  with:
    status: failure
    service: Service.Name
    environment: dev
    slack_webhook: ${{ secrets.SLACK_WEBHOOK_URL }}
