# Sample-Channel

## Setup procedure
1. SignUp for the accoumt at the http://www.github.com/ 
2. Go to apps and create an app 
3. verify 
4. Generate token
5. setup the webhook on the http://www.github.com/webhooks/creat and endpoint url of the bot
6. endpoint url of the bot is added is http://naaniz.com/api/bot/webhooks/mychannel/
7. Add health check url of the bot is http://naaniz.com/api/bot/webhooks/mychannel/health

## Payloads

### Channel Input Message payloads
- #### Text only Input
  ```
  {
  id:"123",
  "message":"hi"
  }
  ```
  - #### Image with Text Input
  ```
  {
  id:"123",
  "message":"hi",
  "image":"<link_image>",
  type:"image/jpg"
  }
  ```
.., so on
  <br>
### Channel Ouput Message/Response payloads
- #### Text only Output
  ```
  {
  sender,
  "message":"hi"
  }
  ```
  - #### Image with Text Output
  ```
  {
    messages:[
    {
      sender:"123",
    "message":"hi",
    "image":"<link_image>",
    type:"image/jpg"
    },
    {
      sender:"123",
      "image":"<link_image>",
      type:"image/jpg"
     }
  ]

  }
  ```
  .., so on
  
  
  <br>
  <br>
  **This is just an example, payloads may contain buttons,quickreplies,text,images,video,documents,location, some other UI also**
  
  
