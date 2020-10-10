# Getting Credentials
* You first have to create a Twilio app to get credentials. Once you have them you can add these to your credentials.yml.
* How to get the Twilio credentials: You need to set up a Twilio account.

* Once you have created a Twilio account, you need to create a new project. The basic important product to select here is Programmable SMS.

* Once you have created the project, navigate to the Dashboard of Programmable SMS and click on Get Started. Follow the steps to connect a phone number to the project.

* Now you can use the Account SID, Auth Token, and the phone number you purchased in your credentials.yml.

* Configure your webhook URL by navigating to Phone Numbers in the Twilio dashboard and selecting your phone number. Find the Messaging section and add your webhook URL (e.g. https://<host>:<port>/webhooks/twilio/webhook, replacing the host and port with the appropriate values from your running Rasa X or Rasa Open Source server) to the A MESSAGE COMES IN setting.
  
 ## Connecting to WhatsApp
* Add the Twilio credentials to your credentials.yml:
twilio:
  account_sid: "ACbc2dxxxxxxxxxxxx19d54bdcd6e41186"
  auth_token: "e231c197493a7122d475b4xxxxxxxxxx"
  twilio_number: "+440123456789"  # if using WhatsApp: "whatsapp:+440123456789"
 
* Restart your Rasa X or Rasa Open Source server to make the new channel endpoint available for Twilio to send messages to.

## Responding to incoming message
const http = require('http');
const express = require('express');
const MessagingResponse = require('twilio').twiml.MessagingResponse;

const app = express();

app.post('/sms', (req, res) => {
  const twiml = new MessagingResponse();

  twiml.message('The Robots are coming! Head for the hills!');

  res.writeHead(200, {'Content-Type': 'text/xml'});
  res.end(twiml.toString());
});

http.createServer(app).listen(1337, () => {
  console.log('Express server listening on port 1337');
});

# Send WhatsApp Notification Messages with Templates
#Download the helper library from https://www.twilio.com/docs/python/install
from twilio.rest import Client


#Your Account Sid and Auth Token from twilio.com/console
#DANGER! This is insecure. See http://twil.io/secure
account_sid = 'ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
auth_token = 'your_auth_token'
client = Client(account_sid, auth_token)

message = client.messages \
    .create(
         from_='whatsapp:+15005550006',
         body='Hi Joe! Thanks for placing an order with us. We’ll let you know once your order has been processed and delivered. Your order number is O12235234',
         to='whatsapp:+14155238886'
     )

print(message.sid)

# WhatsApp Notification categories
* Account Update: Let customers know about updates or changes to their accounts.
* Alert Update: Send important updates or news to customers.
* Appointment Update: Send confirmations, reminders, or other updates to customers about their appointments.
* Auto-Reply: Send auto-replies to customers when your business isn't online or available to respond right away.
* Issue Resolution: Respond to questions, concerns, or feedback from customers about your business.
* Payment Update: Send a message to customers about their payment.
* Personal Finance Update: Send a message to customers about their personal finances.
* Reservation Update: Send confirmations, reminders, or other updates to customers about their reservations.
* Shipping Update: Send shipping updates to customers about their orders.
* Ticket Update: Send ticketing information or updates to customers.
* Transportation Update: Send transportation information or updates to customers.

# Send a WhatsApp message using a template
For example, if your approved template is:
* Hi {{1}}! Thanks for placing an order with us. We’ll let you know once your order has been processed and delivered. Your order number is {{2}}

* in the Body parameter of the message resource, you would write the following, replacing the {{1}} placeholder with the end user's information:
Body=“Hi Joe! Thanks for placing an order with us. We’ll let you know once your order has been processed and delivered. Your order number is O12235234”

# Send and Receive Media Messages with the Twilio API for WhatsApp
#Download the helper library from https://www.twilio.com/docs/python/install
from twilio.rest import Client


#Your Account Sid and Auth Token from twilio.com/console
#DANGER! This is insecure. See http://twil.io/secure
account_sid = 'ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
auth_token = 'your_auth_token'
client = Client(account_sid, auth_token)

message = client.messages \
    .create(
         media_url=['https://images.unsplash.com/photo-1545093149-618ce3bcf49d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=668&q=80'],
         from_='whatsapp:+14155238886',
         body="It's taco time!",
         to='whatsapp:+15017122661'
     )

print(message.sid)
# EXAMPLE JSON API RESPONSE
{
  "account_sid": "ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "api_version": "2010-04-01",
  "body": "It's taco time!",
  "date_created": "Thu, 30 Jul 2015 20:12:31 +0000",
  "date_sent": "Thu, 30 Jul 2015 20:12:33 +0000",
  "date_updated": "Thu, 30 Jul 2015 20:12:33 +0000",
  "direction": "outbound-api",
  "error_code": null,
  "error_message": null,
  "from": "whatsapp:+14155238886",
  "messaging_service_sid": "MGXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "num_media": "0",
  "num_segments": "1",
  "price": null,
  "price_unit": null,
  "sid": "SMXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "status": "sent",
  "subresource_uris": {
    "media": "/2010-04-01/Accounts/ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/Messages/SMXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/Media.json"
  },
  "to": "whatsapp:+15017122661",
  "uri": "/2010-04-01/Accounts/ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/Messages/SMXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX.json"
}

# Guidance on WhatsApp Media Messages
* Message Size Limits For a WhatsApp message, the maximum size limit is 16MB.
* Images: JPG, JPEG, PNG
* Audio: MP3, OGG, AMR
* Documents: PDF
* Video: MP4
# Rich Messaging Features in the Twilio API for WhatsApp
Formatting in WhatsApp Messages
* Bold Asterisk (*  *)
* Italic	Underscore ( _)
* Strike-through	Tilde (~ )
* Code / Pre-formatted	Three backticks (``` )

# Location Messages with WhatsApp
* Sending outbound location messages over WhatsApp is similar to sending a text-based message, with the addition of the PersistentAction parameter in your Twilio API requests, with must include the following information:
* sample payload containing location
*Latitude =37.7879277&Longitude=-122.3937508&Address=375+Beale+St%2C+San+Francisco%2C+CA+94105&SmsMessageSid=SMxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&NumMedia=0&SmsSid=SMxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&Label=Twilio+Inc&Body=&To=whatsapp%3A%2B14155238886&NumSegments=1&MessageSid=SMxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&AccountSid=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&From=whatsapp%3A%2B12345678900&ApiVersion=2010-04-01

# Start conversations with deep links
* Customers can initiate a conversation with you on WhatsApp through URL deep links, such as on your website. If end users have WhatsApp installed on their devices, clicking the deep link opens a conversation with your business inside of WhatsApp.
* Deep link format : whatsapp://send?phone=<e164 number>&text=Hello!

# QR Codes and Short Links
QR codes and short links enable consumers to initiate a conversation with a business without adding a new contact in their phone!
