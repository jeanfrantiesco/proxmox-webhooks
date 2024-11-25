### Telegram WebHook Proxmox
1. [Gettin Started](#getting-started)
2. [WebHook Fields in Proxmox 8.3](#webhook-fields-in-proxmox-83)
3. [Enable Notification Matches](#enable-notification-matches)

## Getting started  
To send messages to Telegram, you need to:

1. Create a bot in Telegram (through BotFather).  
2. Get the `BOT_TOKEN` and `CHAT_ID` for the bot:  
- `BOT_TOKEN`: This is generated when you create the bot with BotFather.
- `CHAT_ID`: This can be obtained by sending a message to the bot and using the Telegram API to get the chat ID (example: `https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates`).

## WebHook Fields in Proxmox 8.3
Add new webhook with following parameters

**1. Endpoint Name**  
Choose name, like: `TelegramWebhook`

**2. Enable**  
Make sure to check the option to enable webhook.  

**3. Method/URL**  
- Method: `POST`
- URL: `https://api.telegram.org/bot{{ secrets.token }}/sendMessage`

**4. Headers**
Add necessary headers for authentication and data format.  
- Header:
  - Key: `Content-Type`
  - Value: `application/json`

**5. Body**  
```
{
  "chat_id": "{{ secrets.chat_id }}",
  "text": "{{message}}"
}
```

**6. Secrets** 
- Secrets 1:
  - Key: `token`
  - Value: `Your_BOT_TOKEN`
- Secrets 2:
  - Key: `chat_id`
  - Value: `Your_CHAT_ID`

**7. Comment** 
- Description: "Webhook for sending notifications to Telegram."

## Enable Notification Matches
Add new **Notification Matches** with following parameters

**1. General**  
- Matcher Name:
  - `<Choose a name>`
- Comment:  
  - `<Choose a comment>`

**2. Match Rules**  
- You don't need to do anything.

**3. Targets to notify**  
- Select the `TelegramWebhook` previously created

## Testing
After configuration, use Proxmox test feature to verify that message arrive.