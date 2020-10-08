# Facebook-Messenger

## Getting Credentials

* To create the app head to [Facebook for Developers](https://developers.facebook.com) and click ```My App``` &#8594; ```Add New App```
* Go to Dashboard for the app under ```Products``` ,find the ```Messenger``` section and click ```Set Up```. 
* Scroll down to ```Token Generation```  and click on the link to create a new page for your app.
* Create your page and select ```Token Generation``` from dropdown. Also copy the ```Page Access Token``` which will be needed later on
* Locate the ```App Secret``` in the app dashboard under ```Settings``` &#8594; ```Basic```. This will be the secret key.
* Use the collected ```secret``` and ```page-access-token``` in the ```credentials.yml```, and add a field called ```verify``` containing a string of your choice. Start ```rasa run``` with the ```--credentials credentials.yml``` option
* Set up a ```Webhook``` and select either ```messaging``` or ```messaging_postback``` subscriptions. Insert your callback URL, which will look like ```https://<host>:<port>/webhooks/facebook/webhook```, replacing the host and port with the appropriate values from Rasa Open Source server.
* Insert the Verify Token which has to match the   
verify entry in your credentials.yml

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
    