### WhatsApp WebHook Proxmox
1. [Gettin Started](#getting-started)
2. [WebHook Fields in Proxmox 8.3](#webhook-fields-in-proxmox-83)
3. [Enable Notification Matches](#enable-notification-matches)

## Getting started  
Setup a API from: https://github.com/chrishubert/whatsapp-api

## WebHook Fields in Proxmox 8.3
Add new webhook with following parameters

**1. Endpoint Name**  
Choose name, like: `WhatsAppWebhook`

**2. Enable**  
Make sure to check the option to enable webhook.  

**3. Method/URL**  
- Method: `POST`
- URL: `https://<YOUR-API-URL>//{{ secrets.api-key }}`

**4. Headers**
Add necessary headers for authentication and data format.  
- Header 1:
  - Key: `accept`
  - Value: `*/*`
- Header 2:
  - Key: `x-api-key`
  - Value: `{{ secrets.api-key }}`
- Header 3:
  - Key: `Content-Type`
  - Value: `application/json`

**5. Body**  
```
{  
  "chatId": "<YourNumber>@c.us",  
  "contentType": "string",  
  "content": "``` {{ escape message }}```"  
}
```

**6. Secrets** 
- Secrets:
  - Key: `api-key`
  - Value: `YourApiKey`

**7. Comment** 
- Description: "Webhook for sending notifications to WhatsApp from API."

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
- Select the `WhatsAppWebhook` previously created

## Testing
After configuration, use Proxmox test feature to verify that message arrive.