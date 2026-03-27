[title]: <> (Creating A Webhook)
[date]: <> (2026/02/25)
[category]: <> (general)

# Creating webhooks

You can create webhooks to subscribe to specific events that occur on GitHub.

## About creating webhooks

You can create webhooks to subscribe to specific events on GitHub that occur in a repository, organization, GitHub Marketplace account, GitHub Sponsors account, or GitHub App.

For more information about the different types of webhooks, see [Types of webhooks](/en/webhooks/types-of-webhooks).

For a complete list of webhook events, see [Webhook events and payloads](/en/webhooks/webhook-events-and-payloads).

## Creating a repository webhook

You can create a webhook to subscribe to events that occur in a specific repository. You must be a repository owner or have admin access in the repository to create webhooks in that repository.

You can use the GitHub web interface or the REST API to create a repository webhook. For more information about using the REST API to create a repository webhook, see [REST API endpoints for repository webhooks](/en/rest/webhooks/repos#create-a-repository-webhook).

1. On GitHub, navigate to the main page of the repository.
2. Under your repository name, click **Settings**. If you cannot see the "Settings" tab, select the dropdown menu, then click **Settings**.
3. In the left sidebar, click **Webhooks**.
4. Click **Add webhook**.
5. Under "Payload URL", type the URL where you'd like to receive payloads.
6. Optionally, select the **Content type** drop-down menu, and click a data format to receive the webhook payload in.
    
    * **application/json** will deliver the JSON payload directly as the body of the `POST` request.
    * **application/x-www-form-urlencoded** will send the JSON payload as a form parameter called `payload`.
7. Optionally, under "Secret", type a string to use as a `secret` key. You should choose a random string of text with high entropy. You can use the webhook secret to limit incoming requests to only those originating from GitHub. For more information, see [Validating webhook deliveries](/en/webhooks/using-webhooks/securing-your-webhooks).
8. Under "Which events would you like to trigger this webhook?", select the webhook events that you want to receive. You should only subscribe to the webhook events that you need.
9. If you chose **Let me select individual events**, select the events that you want to trigger the webhook.
10. To make the webhook active immediately after adding the configuration, select **Active**.
11. Click **Add webhook**.

After you create a new webhook, GitHub will send you a simple `ping` event to let you know you've set up the webhook correctly. For more information, see [Webhook events and payloads](/en/webhooks/webhook-events-and-payloads#ping).

## Creating an organization webhook

You can create a webhook to subscribe to events that occur in a specific organization. You must be an organization owner to create webhooks in that organization.

You can use the GitHub web interface or the REST API to create an organization webhook. For more information about using the REST API to create an organization webhook, see [REST API endpoints for organization webhooks](/en/rest/orgs/webhooks#create-an-organization-webhook).

1. In the upper-right corner of any page on GitHub, click your profile picture.
2. Click **Your organizations**.
3. To the right of the organization, click **Settings**.
4. In the left sidebar, click **Webhooks**.
5. Click **Add webhook**.
6. Under "Payload URL", type the URL where you'd like to receive payloads.
7. Optionally, select the **Content type** drop-down menu, and click a data format to receive the webhook payload in.  
    
    * **application/json** will deliver the JSON payload directly as the body of the `POST` request.
    * **application/x-www-form-urlencoded** will send the JSON payload as a form parameter called `payload`.
8. Optionally, under "Secret", type a string to use as a `secret` key. You should choose a random string of text with high entropy. You can use the webhook secret to limit incoming requests to only those originating from GitHub. For more information, see [Validating webhook deliveries](/en/webhooks/using-webhooks/securing-your-webhooks).
9. Under "Which events would you like to trigger this webhook?", select the types of webhooks you'd like to receive. You should only subscribe to the webhook events that you need.
10. If you chose **Let me select individual events**, select the events that will trigger the webhook.
11. To make the webhook active immediately after adding the configuration, select **Active**.
12. Click **Add webhook**.

After you create a new webhook, GitHub will send you a simple `ping` event to let you know you've set up the webhook correctly. For more information, see [Webhook events and payloads](/en/webhooks/webhook-events-and-payloads#ping).

## Creating a GitHub Marketplace webhook

You can create a webhook to subscribe to events relating to an app that you published in GitHub Marketplace. Only the owner of the app, or an app manager for the app, can create a GitHub Marketplace webhook.

1. Navigate to your [GitHub Marketplace listing page](https://github.com/marketplace/manage).
2. Next to the GitHub Marketplace listing that you want to view webhook deliveries for, click **Manage listing**.
3. In the sidebar, click **Webhook**.
4. Under "Payload URL", type the URL where you'd like to receive payloads.
5. Optionally, select the **Content type** drop-down menu, and click a data format to receive the webhook payload in.  
    
    * **application/json** will deliver the JSON payload directly as the body of the `POST` request.
    * **application/x-www-form-urlencoded** will send the JSON payload as a form parameter called `payload`.
6. Optionally, under "Secret", type a string to use as a `secret` key. You should choose a random string of text with high entropy. You can use the webhook secret to limit incoming requests to only those originating from GitHub. For more information, see [Validating webhook deliveries](/en/webhooks/using-webhooks/securing-your-webhooks).
7. To make the webhook active immediately after adding the configuration, select **Active**.
8. Click **Create webhook**.

After you create a new webhook, GitHub will send you a simple `ping` event to let you know you've set up the webhook correctly. For more information, see [Webhook events and payloads](/en/webhooks/webhook-events-and-payloads#ping).

## Creating a GitHub Sponsors webhook

You can create a webhook to subscribe to events relating to your sponsorships. Only the owner of the sponsored account can create sponsorship webhooks for that account. For more information about the event that a sponsorship webhook is subscribed to, see the `sponsorship` [webhook event](/en/webhooks-and-events/webhooks/webhook-events-and-payloads#sponsorship).

1. In the upper-right corner of any page, click your profile picture, then click **Your sponsors**.
2. Next to the account you want to create a webhook for, click **Dashboard**.
3. In the left sidebar, click **Webhooks**.
4. Click **Add webhook**.
5. Under "Payload URL", type the URL where you'd like to receive payloads.
6. Optionally, select the **Content type** drop-down menu, and click a data format to receive the webhook payload in.  
    
    * **application/json** will deliver the JSON payload directly as the body of the `POST` request.
    * **application/x-www-form-urlencoded** will send the JSON payload as a form parameter called `payload`.
7. Optionally, under "Secret", type a string to use as a `secret` key. You should choose a random string of text with high entropy. You can use the webhook secret to limit incoming requests to only those originating from GitHub. For more information, see [Validating webhook deliveries](/en/webhooks/using-webhooks/securing-your-webhooks).
8. To make the webhook active immediately after adding the configuration, select **Active**.
9. Click **Create webhook**.

## Creating webhooks for a GitHub App

The owner of a GitHub App can subscribe the app to webhook events to receive notifications whenever certain events occur. If the app owner has designated any app managers for a GitHub App, the app managers can also subscribe the app to webhook events. For more information, see [Using webhooks with GitHub Apps](/en/apps/creating-github-apps/creating-github-apps/using-webhooks-with-github-apps).

Each GitHub App has one webhook. You can configure the webhook when you register a GitHub App, or you can edit the webhook configuration for an existing GitHub App registration.

For more information about configuring a webhook when you register a GitHub App, see [Registering a GitHub App](/en/apps/creating-github-apps/registering-a-github-app/registering-a-github-app).

To configure a webhook for an existing GitHub App registration:

1. In the upper-right corner of any page on GitHub, click your profile picture.
2. Navigate to your account settings.
    
    * For an app owned by a personal account, click **Settings**.
    * For an app owned by an organization:  
        
        1. Click **Your organizations**.
        2. To the right of the organization, click **Settings**.
3. In the left sidebar, click **Developer settings**.
4. In the left sidebar, click **GitHub Apps**.
5. Next to the GitHub App that you want to configure the webhook for, click **Edit**.
6. Under "Webhook," select **Active**.
7. Under "Webhook URL", type the URL where you'd like to receive payloads.
8. Optionally, under "Webhook secret", type a string to use as a `secret` key. You should choose a random string of text with high entropy. You can use the webhook secret to limit incoming requests to only those originating from GitHub. For more information, see [Validating webhook deliveries](/en/webhooks/using-webhooks/securing-your-webhooks).
9. Click **Save changes**.
10. In the sidebar, click **Permissions & events**.
11. The specific webhook events that you can select for your GitHub App registration are determined by the type of permissions you selected for your app. You will first need to select the permissions you would like your app to have, and then you can subscribe your app to webhook events that are related to that set of permissions.
    
    Under the sections "Repository permissions," "Organization permissions," and "Account permissions," select the permissions that are required for the events your app will subscribe to. For more information, see [Choosing permissions for a GitHub App](/en/apps/creating-github-apps/creating-github-apps/choosing-permissions-for-a-github-app). For more information about things to consider when changing the permissions, see [Modifying a GitHub App registration](/en/apps/maintaining-github-apps/modifying-a-github-app-registration#changing-the-permissions-of-a-github-app).
12. Under "Subscribe to Events," select the webhook events you would like your GitHub App to receive.
13. Click **Save changes**.

You can also use the REST API to create a webhook for a GitHub App. For more information, see [REST API endpoints for GitHub App webhooks](/en/rest/apps/webhooks).

## Further reading

* [About webhooks](/en/webhooks/about-webhooks)
* [Handling webhook deliveries](/en/webhooks/using-webhooks/handling-webhook-deliveries)