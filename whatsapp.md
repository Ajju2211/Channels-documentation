# Getting Credentials
*You first have to create a Twilio app to get credentials. Once you have them you can add these to your credentials.yml.
*How to get the Twilio credentials: You need to set up a Twilio account.

*Once you have created a Twilio account, you need to create a new project. The basic important product to select here is Programmable SMS.

*Once you have created the project, navigate to the Dashboard of Programmable SMS and click on Get Started. Follow the steps to connect a phone number to the project.

*Now you can use the Account SID, Auth Token, and the phone number you purchased in your credentials.yml.

*Configure your webhook URL by navigating to Phone Numbers in the Twilio dashboard and selecting your phone number. Find the Messaging section and add your webhook URL (e.g. https://<host>:<port>/webhooks/twilio/webhook, replacing the host and port with the appropriate values from your running Rasa X or Rasa Open Source server) to the A MESSAGE COMES IN setting.
  
 ##Connecting to WhatsApp
*Add the Twilio credentials to your credentials.yml:
twilio:
  account_sid: "ACbc2dxxxxxxxxxxxx19d54bdcd6e41186"
  auth_token: "e231c197493a7122d475b4xxxxxxxxxx"
  twilio_number: "+440123456789"  # if using WhatsApp: "whatsapp:+440123456789"
 
*Restart your Rasa X or Rasa Open Source server to make the new channel endpoint available for Twilio to send messages to.

##Responding to incoming message
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
