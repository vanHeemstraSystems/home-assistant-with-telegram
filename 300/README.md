# 300 - Building Our Application

So if we navigate to the Home assistant telegram integration (https://home-assistant.io/integrations/telegram) there are some detailed instructions that will guide us us through the installation process.

First off there are a few obvious prerequisites that we'll need a telegram account and have to set it up on a device. This is a totally free and for the purposes of this demonstration we'll be doing this on a Windows desktop version.

To install this navigate to https://telegram.org. Search for and select the telegram for PC and Linux. Press the **get telegram for windows x64**. Open the file. 

Once it's downloaded, select your language. Select destination and press okay. Select the start menu folder. Create a desktop icon and press install. 

**NOTE**: Remember to tick ```launch Telegram``` and finish. 

Now let's start messaging. 

If you have telegram already installed onto a mobile device you can scan the QR code from within that device application and link it automatically or log in using your mobile phone number. Enter your mobile phone number. Press next you'll receive a code on your mobile phone number. Enter this code in here you'll be directed to the main chat screen for telegram. So what we need now is a telegram bot this is a cool way that telegram can process inputs and requests from users such as turning on the lights and then informing you in this has been done but for the purposes of this video we'll be sending messages from home assistant to telegram. 

To be able to send messages from home assistant to telegram will need to create a bot telegram. Bots are actually pretty simple to create. In search field search for atbf father make sure that this is the one with the blue tick to the right and there are quite a few that are listed. Select this and press start. This will bring up a full list of commands that you can action on this bot. 

We want to select the new bot. You will be prompted to give the bot a name you'll be prompted to give the bot a username. I'd recommend using the same name that you created the bot, but using an underscore bot at the end of it. For the username atbot father will give you the congratulation message but the only thing we need here is the key.

Copy this and paste it somewhere safe. Now we need to get the chat ID for yourself. To do this we'll need to talk to another bot called get IDs. Navigate to the search in the top left of telegram and search and select for get IDs. Select get IDs bot press the start message in your Bot the bot will return your ID information. 

The number that you're looking for is the ID number. Copy this and paste it along with the API key information somewhere safe. Now let's start up our bot in telegram search for it. In the search bar select it and press start. At the time of recording I'm running on home assistant core version 2023 do111. We'll need to make a change to our configuration.yaml file.

To do this we'll need a file editor. I'd recommend using Studio code server. You can follow along with my installation and configuration video in the link above or in the descriptions below. 

Navigate to Studio code server select your configuration.yaml file. Navigate back to the home assistant telegram web page. Link in the description below. Scroll down till you reach the configuration section press the copy button navigate back into home assistant. 

Select an appropriate space paste that code in the telegram bot remove the chat IDs one to three insert into this section the chat ID number that you copied from before. 

I'll just use a dummy number in this case replace the text for your API key with the API key that was provided by the bopf Father the chat ID underneath the notify for the second chat is not required and can be removed in the notify command replace the chat ID with the number that you copied above in the allowed chat IDs and we're finished we can SA save this by exiting out with an ex while home assistant can send telegram messages it can't send messages to any person it can only send messages to users who have invited a conversation with the bot and whose chat ID is known check the home assistant telegram web page for the limitations of whom telegram can message now I'd recommend that you store your API key and your ID in your secret. yaml file I've used dummy values for obvious reasons but if you'd like a V but if You' like a video on the secrets.yaml file and how to use it then let me know in the comments below

Now let's restart home assistant navigate to developer tools check your configuration press restart confirm restart and again now let's wait for home assistant to come back now let's send a message to our telegram bot select Services search for and select telegram bot and select now this has been vastly improved in recent revisions of home assistance so the old method of having to code a message has gone and it's now much more like the way to send notifications to home assistant companion app so let's give it a message and send it type in a message optionally it give it a title now press call service the message will appear in the telegram chat window that you started likewise you can call this service from your automations as you would with sending notification messages you can also send photos videos sound Clips to your telegram all with no size limitations a put in the link description to everything talked about to help with your simple installation so there you have it a way of sending messages to yourself via the telegraph app and also to be able to send messages to the telegram app independently of having home assistant app there is a lot more that you can do with telegram integration and we have only skimmed the surface read through the documentation for yourself and if you'd like a dedicated Deep dive video on Telegram then let me know in the comments below enjoy sending those telegram messages until the next one
