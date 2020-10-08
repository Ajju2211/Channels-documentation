# Facebook-Messenger

## Getting Credentials

* To create the app head to [Facebook for Developers](https://developers.facebook.com) and click ```My App``` &#8594; ```Add New App```
* Create a page on facebook or You can use existing page.
* Go to Dashboard for the app under ```Products``` ,find the ```Messenger``` section and click ```Set Up```. 
* Scroll down to ```Token Generation```  and click on the link to create a new page for your app.
* Create your page and select ```Token Generation``` from dropdown. Also copy the ```Page Access Token``` which will be needed later on
* Locate the ```App Secret``` in the app dashboard under ```Settings``` &#8594; ```Basic```. This will be the secret key.
* Use the collected ```secret``` and ```page-access-token``` in the ```credentials.yml```, and add a field called ```verify``` containing a string of your choice. Start ```rasa run``` with the ```--credentials credentials.yml``` option
* Set up a ```Webhook``` and select either ```messaging``` or ```messaging_postback``` subscriptions. Insert your callback URL, which will look like ```https://<host>:<port>/webhooks/facebook/webhook```, replacing the host and port with the appropriate values from Rasa Open Source server.
* Insert the Verify Token which has to match the verify entry in your credentials.yml

## Credential.yml contents

* ```
  facebook:
    verify: <some string>
    secret: <secret-token>
    page-access-token: <page-access-token>```

## Supported Responses | Attachments

* ##### Buttons :- 
  * same as rasa buttons but facebook api restrict to only 3 buttons per messages. All other buttons will be ignored

* ##### Quick Replies :-
  * Support upto 13 buttons in conversation. 
  * ###### The following quick reply types are supported :-
    * Text
    * Phone Number
    * Email


## Payload :-

* #### quick_replies :-
  
    * Type text
    ```
       {
           "message":
                {
                    "text":"Pick a color:",
                    "quick_replies":
                    [
                        {
                            "content_type":"text",
                            "title":"Red",
                            "payload":"<POSTBACK_PAYLOAD>",
                            "image_url":"example1.png"
                        }
                    ]
                }
        }
    ```

    * Quick Reply Type Email
    ```
    {
        "content_type":"user_email"
    }
         
    ```

    * Quick Reply Type Phone Number 
    ```
    {
        "content_type":"user_phone_number"
    }
    ```   

* #### Airline Template :-

```
{
  
  "message": {
    "attachment": {
      "type": "template",
      "payload": {
        "template_type": "airline_update",
        "intro_message": "Your flight is delayed",
        "update_type": "delay",
        "locale": "en_US",
        "pnr_number": "CF23G2",
        "update_flight_info": {
          "flight_number": "KL123",
          "departure_airport": {
            "airport_code": "SFO",
            "city": "San Francisco",
            "terminal": "T4",
            "gate": "G8"
          },
          "arrival_airport": {
            "airport_code": "AMS",
            "city": "Amsterdam",
            "terminal": "T4",
            "gate": "G8"
          },
          "flight_schedule": {
            "boarding_time": "2015-12-26T10:30",
            "departure_time": "2015-12-26T11:30",
            "arrival_time": "2015-12-27T07:30"
          }
        }
      }
    }
  }
}
```

* #### List Template : -
    *
```
"payload": {
  "template_type": "list",
  "top_element_style": "<LARGE | COMPACT>",
  "elements": [
    {
      "title": "<TITLE_TEXT>",
      "subtitle": "<SUBTITLE_TEXT>",
      "image_url": "<IMAGE_URL_FOR_THUMBNAIL>",          
      "buttons": [<BUTTON_OBJECT>],
      "default_action": {
        "type": "web_url",
        "url": "<URL_TO_OPEN_WHEN_ITEM_IS_TAPPED>",
        "messenger_extensions": <TRUE | FALSE>,
        "webview_height_ratio": "<COMPACT | TALL | FULL>"
      }
    },
    ...
  ],
   "buttons": [<BUTTON_OBJECT>]  
}
```

* #### Media Template :-
```
{
  
  "message":
    {
        "attachment": 
        {
             "type": "template",
              "payload": 
            {
                  "template_type": "media",
                  "elements": [
                        {
                          "media_type": "<image|video>","url": "<FACEBOOK_URL>"
                        }
                ]
            }
        }    
    }
}
```

* #### Product Template :-
```
"payload": 
{
    "template_type":"product",
    "elements":[
        {
            "id":<PRODUCT_ID>
        },
    ]
}
```
* #### Generic Template (for carroussel) :-

```
curl -X POST -H "Content-Type: application/json" -d '{
  "recipient":{
    "id":"<PSID>"
  },
  "message":{
    "attachment":{
      "type":"template",
      "payload":{
        "template_type":"generic",
        "elements":[
           {
            "title":"Welcome!",
            "image_url":"https://petersfancybrownhats.com/company_image.png",
            "subtitle":"We have the right hat for everyone.",
            "default_action": {
              "type": "web_url",
              "url": "https://petersfancybrownhats.com/view?item=103",
              "webview_height_ratio": "tall",
            },
            "buttons":[
              {
                "type":"web_url",
                "url":"https://petersfancybrownhats.com",
                "title":"View Website"
              },{
                "type":"postback",
                "title":"Start Chatting",
                "payload":"DEVELOPER_DEFINED_PAYLOAD"
              }              
            ]      
          }
        ]
      }
    }
  }
}' "https://graph.facebook.com/v2.6/me/messages?access_token=<PAGE_ACCESS_TOKEN>"

```

Response
```
{
  "recipient_id": "1254477777772919",
  "message_id": "AG5Hz2Uq7tuwNEhXfYYKj8mJEM_QPpz5jdCK48PnKAjSdjfipqxqMvK8ma6AC8fplwlqLP_5cgXIbu7I3rBN0P"
}
```


