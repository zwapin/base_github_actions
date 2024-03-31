# Send Notification to Slack Commits Channel

This GitHub Action sends a custom notification to your internal Slack channel whenever a new commit is pushed. It allows you to include a custom emoji in the message, enhancing the visual appeal and immediacy of the notification.

## Inputs

- `emoji`: (Optional) The emoji related to your repository that will be displayed in the Slack message. If not specified, the default emoji is ":question:".
- `slack-webhook-url`: **Required**. The URL of the Slack Incoming Webhook to which the notification will be sent. 

## How to Use

To use this action in your workflow, follow these steps:

1. **Create a Slack App and Incoming Webhook**
   
   If you haven't already, create a Slack app and set up an incoming webhook in your Slack workspace. Slack provides [detailed documentation](https://api.slack.com/messaging/webhooks) on this process.

2. **Add the Webhook URL to Your GitHub Secrets**

   Navigate to your repository's Settings > Secrets and add your Slack webhook URL as a new secret. This ensures that your webhook URL remains secure. Name it something memorable, like `SLACK_WEBHOOK_URL`.

3. **Configure the Workflow**

   In your repository, create or edit a workflow file (e.g., `.github/workflows/notify-slack.yml`) and add a step to use this action. Here's a sample configuration:

   ```yaml
   name: Notify Slack on Commit
   on: push

   jobs:
     notify-slack:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@v2
         
         - name: Send Slack Notification
           uses: zwapin/base_github_actions/notificate-commit-action@master
           with:
             emoji: ':tada:' # Optional
             slack-webhook-url: ${{ secrets.SLACK_WEBHOOK_URL }}
    ```

## Customization

You can change the emoji input to any emoji that best represents the context of your notification. This could be related to the type of commit, the branch, or just to add a fun element to your notifications.

The message template can be modified directly in the action.yml file if different information or formatting is desired for the notification.

## Security Considerations
Make sure to keep your slack-webhook-url secret and only use it in secure contexts.
Regularly review your Slack app's permissions and the channels it has access to, ensuring it aligns with your security and privacy policies.
