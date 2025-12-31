## Available Workflows templates

### Pull Request Opened Notification

This workflow triggers automatically when a Pull Request reaches a reviewable state.

Trigger events include:
- Pull Request opened
- Pull Request reopened
- Pull Request marked as ready for review

Execution conditions:
- The Pull Request targets the main branch (for example, main or master)
- At least one reviewer is requested

Purpose:
Notify a Slack channel that a Pull Request is ready for review, reducing manual coordination and improving review flow visibility.

This workflow is fully event-driven and does not require user interaction.

---

### Pull Request Notification via Comment (/send-review)

This workflow is triggered when a comment is added to a Pull Request.

It listens for a specific command issued as a comment:
- /send-review
- Optionally followed by a custom title

Behavior:
- Detects whether the comment contains the trigger command
- Optionally extracts a custom title provided by the author
- Fetches Pull Request metadata directly from GitHub
- Triggers a reusable notification workflow if conditions are met

Purpose:
Allow developers to manually notify Slack when:
- A Pull Request is ready for review but was not caught by automation
- A PR needs renewed attention
- A custom context or title should be provided in the notification

This workflow complements the automatic approach by giving developers explicit control.

---

## Reusable Workflow Architecture

Both workflows delegate the actual Slack notification logic to a reusable workflow.

This design:
- Centralizes Slack formatting and delivery
- Avoids duplication across repositories
- Simplifies maintenance and updates
- Keeps public workflows free of sensitive or organization-specific logic

Repositories using these workflows are responsible for:
- Referencing the reusable workflow
- Providing the required inputs
- Configuring the required secrets

---

## Required Secrets

The workflows depend on secrets defined in the consumer repository.

Required secret:
- SLACK_WEBHOOK_URL  
  Slack Incoming Webhook URL used to send notifications.

No secrets are stored, hard-coded, or exposed in this repository.

---