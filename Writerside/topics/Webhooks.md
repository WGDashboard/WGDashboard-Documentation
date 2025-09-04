# Webhooks

## Create Webhooks

1. Once you opened WGDashboard, you should see a new menu item in the navigation bar called **Webhooks**, click on it to open the webhooks manager.
2. If you're first time using it, you should see a blank page, which is normal. **To create a new webhook, click on the blue button in the top right corner.**
3. Fill in the form
   1. **Payload URL**: This is the URL WGDashboard will post to, it can be HTTP or HTTPS
   2. **Content Type**: This depends on how you want to receive data, in JSON format, or URL encoded format
   3. **Verify SSL**: This only applies if your **Payload URL** is **HTTPS**, we strongly recommend to keep this on so we can make sure your data is not sent to bad people ;)
   4. **Custom Headers**: If your **Payload URL** required extra headers, like API Keys, Bearer token, you can do so.
   5. **Subscribed Actions**: You can choose which event(s) you want to subscribe. In the future we will add more actions.
   6. **Enable Webhook**: You can choose to enable it or not after saving it
4. Click **Save** and voila your Webhook is ready!

## Payload Example

```json
{
    "configuration": "Aa1",
    "peers": [
        "D2F7tP1sXbhT7ye2tl4aDoBk+tpiOZAvU4Jw8Jt3W0g="
    ],
    "action": "peer_created",
    "time": "2025-09-03 17:10:51",
    "webhook_id": "b1d5a1b1-b2e5-430d-a366-076a50300cdc",
    "webhook_session": "2d6d536d-2e7a-4382-9c20-339c68148cdc"
}
```
Webhook payloads will only expose public information, keys in `$.peers` are their public key