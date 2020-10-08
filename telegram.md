# Telegram 

## Create a New Bot and Token in Telegram

* [Create a new Telegram bot](https://telegram.me/botfather) using the Bot Father.
* To create a new Telegram bot, send command ```/newbot```
* Click on ```Create new project``` and create a new project from scratch.
* Give the Telegram bot a unique username.
* Your new app should appear in your apps list. Click on the app’s name to enter the Chatflow editor.
* To make your app nice and tidy, you can enable grid in the ```Settings/view``` menu.
* Drag the ```Telegram In``` and ```Telegram Out``` nodes from the Node Library to your bot’s ChatFlow canvas and then connect them with a wire
* If the Telegram In and Telegram Out nodes are not in your Node Library, click on ```Settings``` in the right hand corner. A drop down will open. Click on ```Node Installer```
* In the Node Installer, search for Telegram. Click on the blue arrow to the right of Telegram to add the nodes into your palette

## Configure The Bot

* Double click the Telegram In Node, select ```Add new selectbot-controller…```, and click the ```Edit``` button.
* Enter your ```Telegram Bot Token``` name under the ```Name``` field (ex. Echo Bot). Name your ```Telegram Bot Token``` to save it. This will allow that configuration to be used by other nodes.
* Paste the Token you copied from BotFather into the Token field. Click the ```Add``` button.
* Double click on the Telegram Out Node and select the ```Echo Bot``` Token. Click okay.


## Deploy the Application

* Click on ```deploy``` button in the upper right hand corner to deploy your application.
* After the application is deployed, your bot should be online.


## Telegram In and Telegram Out Nodes

* Telegram In
``` 
{
payload: payload,
 telegram: {
             message: message,
             user: message.from,
             chat: message.chat,
             type: message.type,
             // optional fields:
             location: message.location,
             venue: message.location,
             image: message.photo,
             contact: message.contact
           },
 kitt: {
         _session_id: message.from.id,
         _user_id: message.from.username,
         _timeout: 120
       }
 }
 ```
 
 
 * Telegram Out
 ```
 msg = {payload: payload,
       telegram: {user: user,
                  chat: chat,
                  type: type
                  }
      }
 ```
      
      
* To send text message 
 ```
msg = {payload: "Hello there",
       telegram: {
                   user: {id: "user-id"},
                   type: "text"
                   }
       }
 ```
       
       
* To send location
 ```
msg = {payload: {
                 latitude: 1.1111,
                 longitude: 1.1111
                 },
       telegram: {
                 user: {id: "user-id"},
                 type: "location"
                 }
       }
 ```
       
       
* To send a venue
 ```
msg = {payload: {
                 title: "venue title",
                 address: "venue address",
                 id: "unique id",
                 latitude: 1.1111,
                 longitude: 1.1111
                 },
       telegram: {
                 user: {id: "user-id"},
                 type: "location"
                 }
       }
  ```
       
       
* To send an image
 ```
msg = {
       payload: "http://server.com/image.png",
       telegram: {
                 user: {id: "user-id"},
                 type: "image"
                 }
       }
 ```
       
       
* To send a sticker
```
msg = {
       payload: "http://server.com/sticker.png",
       telegram: {
                 user: {id: "user-id"},
                 type: "sticker"
                 }
       }
 ```
       
       
* To respond to an inline inquery
 ```
msg = {
       payload: InlineQueryResults,
       telegram: {
                   user: {id: "user-id"},
                           type: "inline_query"
                 }
       }
 ```
  
  
  ## The Setup
  * Download the ```JSON file``` for our application and import the project on the applications page
  * Acquire the Bot Token 
