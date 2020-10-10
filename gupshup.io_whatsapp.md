# Channels-documentation
This is the custom payloads documentation of very channels. 
You can also integrate with third party services such as an NLP tool, through the IDE Bot Builder. As an advanced user, you can have control for custom hosting of your bot using the 'Callback URL' option to specify the endpoint where your bot logic resides.
# Building a bot outside Bot Builder tool.
Gupshup allows you to write the bot code outside Gupshup's Bot Builder tool in any programming language of your choice.You can then associate a callback to the bot on Gupshup's platform.This callback will be the location of your bot code on the server where you have hosted the code. Whenever the bot is called by the user, Gupshup will send the relevant details to your bot through the callback URL using which you can respond back to the user.
1.  Create a bot on Gupshup platform - Go to My Bots section and then click on the '+' sign on the bottom right and give a name to the bot.
2.  Write the bot's code in your IDE -
When a user interacts with the bot a GET call is made to the callback URL with additional parameters
Pseudo code 
*   String URL is url of  is external chatbot api

JSONObject messageobjObj = JSONObject(messageobj)
String conversationType = messageobjObj.getString("type");
String cityName = messageobjObj.getString("text");
if(conversationType.equalsIgnoreCase("msg"))
{
  String URL = "https://api.worldweatheronline.com/free/v2/weather.ashx?q="+cityName+"&format=json&num_of_days=1&key={Your apikey}";

  okhttp3.OkHttpClient client = new okhttp3.OkHttpClient();
  okhttp3.Request request = new okhttp3.Request.Builder()
                              .url(URL)
                              .get()
                              .build();
  okhttp3.Response response = client.newCall(request).execute();
  
  ## mmediate response
  In this you return a HTTP response back to the callback without any delay.
  Pseudo code

response.setContentType("text/html"); 
PrintWriter out = response.getWriter();
out.print("Weather in"+cityName+" is -"+responseofWeatherAPI);
out.flush();
out.close();
## Delayed response 
In this you can use the Gupshup send message API.
Pseudo code
String botname = "weatherbot";
String botmessage = "Weather in"+cityName+" is -"+responseofWeatherAPI";
String URL = "http://api.gupshup.io/sm/api/bot/weatherbot/msg";
String body = "apikey={Your Gupshup API key}&botname="+botname+"&context="+contextobj+"&message="+botmessage;
okhttp3.OkHttpClient client = new okhttp3.OkHttpClient();
okhttp3.MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(mediaType,body);
okhttp3.Request request = new okhttp3.Request.Builder()
                           .url(URL)
                           .post(body)
                           .build();
okhttp3.Response response = client.newCall(request).execute();

## Deploy locally and associate the callback
To deploy the bot locally 

## Testing your bot 
You can test your bot either using the Proxy Bots or you can publish your bot to the specific messaging channel and test.
