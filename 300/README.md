# 300 - Building Our Application

So if we navigate to the Home assistant telegram integration (https://home-assistant.io/integrations/telegram) there are some detailed instructions that will guide us us through the installation process.

First off there are a few obvious prerequisites that we'll need: 
- a Telegram account
- and have to set it up on a device. 

This is a totally free and for the purposes of this demonstration we'll be doing this on a Windows desktop version and Mac OS desktop version.

To install this navigate to https://telegram.org. 

- Search for and select the telegram for PC and Linux. Press the **Get Telegram for Windows x64**. Open the file.
- Search for and select the telegram for macOS. Press the **Get Telegram for macOS** button. Open the file.

Once it's downloaded, select your language. Select destination and press okay. Select the start menu folder. Create a desktop icon and press install. 

**NOTE**: Remember to tick ```launch Telegram``` and finish. 

Now let's start messaging. 

If you have telegram already installed onto a mobile device you can scan the QR code from within that device application and link it automatically or log in using your mobile phone number. 

Enter your mobile phone number. 

Press **Next**. You'll receive a code on your mobile phone number. 

**NOTE**: Should you not have access to your mobile phone, you can alternatively read the messages through the web interface of Telegram at https://web.telegram.org. 

Enter this code in here. You'll be directed to the main chat screen for telegram. 

So what we need now is a Telegram Bot.

This is a cool way that telegram can process inputs and requests from users such as turning on the lights and then informing you in this has been done, but for the purposes of this video we'll be sending messages from Home Assistant to Telegram. 

To be able to send messages from Home Assistant to Telegram will need to create a Bot. Telegram Bots are actually pretty simple to create. 

In search field search for **@botfather**. Make sure that this is the one with the blue tick to the right and there are quite a few that are listed. 

Select this and press **start**. 

**NOTE**: If you already have created Bots previously, just send the following message to BotFather: ```/start```.

This will bring up a full list of commands that you can action on this bot. 

We want to select the **/new bot**. 

You will be prompted to give the bot a name (here: ```HomeAssistant```). You'll be prompted to give the bot a username (here: ```HomeAssistantX_bot```). 

**NOTE**: Due to ```HomeAssistant_bot``` already having been taken, we opted to add the ```X``` in the name.

I'd recommend using the same name that you created the bot, but using an ```_bot``` at the end of it. For the username **@BotFather** will give you the congratulation message but the only thing we need here is the **key** (here: 6488695438:AAF...........). We can find the new bot at [t.me/HomeAssistantX_bot](https://t.me/HomeAssistantX_bot).

Copy this and paste it somewhere safe. 

For a description of the Bot API, see this page: https://core.telegram.org/bots/api

Now we need to get the **chat ID** for yourself. To do this we'll need to talk to another bot called **GetIDs Bot**. Navigate to the search in the top left of telegram and search and select for **getids**. Select **GetIDs Bot**, press the start message in your Bot. The bot will return your ID information.

The number that you're looking for is the **id** number (here: 6791..........). Copy this and paste it along with the **API key** information somewhere safe. 

Now let's start up our bot in Telegram. Search for it (here: ```HomeAssistantX_bot```). In the search bar select it and press **start**. 

At the time of recording I'm running on Home Assistant Core version 2023.11.1. We'll need to make a change to our ```configuration.yaml``` file.

To do this we'll need a file editor. I'd recommend using ```Studio Code Server```. You can follow along with my installation and configuration video in the link above or in the descriptions below. 

Navigate to ```Studio Code Server```. Select your ```configuration.yaml``` file. Navigate back to the Home Assistant Telegram web page (https://home-assistant.io/integrations/telegram). Scroll down till you reach the **Configuration** section. 

```
# Example configuration.yaml entry for the Telegram Bot
telegram_bot:
  - platform: polling
    api_key: YOUR_API_KEY
    allowed_chat_ids:
      - CHAT_ID_1 # example: 123456789 for the chat_id of a user
      - CHAT_ID_2 # example: -987654321 for the chat_id of a group
      - CHAT_ID_3

# Example configuration.yaml entry for the notifier
notify:
  - platform: telegram
    name: NOTIFIER_NAME
    chat_id: CHAT_ID_1

  # It is possible to add multiple notifiers by using another chat_id
  # the example belows shows an additional notifier which sends messages to the bot which is added to a group
  - platform: telegram
    name: NOTIFIER_NAME_OF_GROUP
    chat_id: CHAT_ID_2
```

Press the **copy** button. 

Navigate back into Home Assistant. 

Select an appropriate space. Paste that code in the ```configuration.yaml``` file. Remove the ```CHAT_ID_``` 1 to 3. Insert into this section the ***chat ID number*** that you copied from before (here: 6791..........).

Replace the text for your **API key** with the **API key** that was provided by the ```Bot Father``` (here: 6488695438:AAF...........). 

The ```chat ID``` underneath the notify for the second chat is not required and can be removed:

```
# Example configuration.yaml entry for the Telegram Bot
telegram_bot:
  - platform: polling
    api_key: 6488695438:AAF...........
    allowed_chat_ids:
      - 6791..........

# Example configuration.yaml entry for the notifier
notify:
  - platform: telegram
    name: NOTIFIER_NAME
    chat_id: CHAT_ID_1
```

In the ```notify``` command replace ```CHAT_ID_1``` with the number that you copied above in the allowed chat IDs and we're finished.

```
# Example configuration.yaml entry for the Telegram Bot
telegram_bot:
  - platform: polling
    api_key: 6488695438:AAF...........
    allowed_chat_ids:
      - 6791..........

# Example configuration.yaml entry for the notifier
notify:
  - platform: telegram
    name: NOTIFIER_NAME
    chat_id: 6791..........
```

We can save this by exiting out with an "x".

While Home Assistant can send Telegram messages, it can't send messages to any person. It can only send messages to users who have invited a conversation with the bot and whose chat ID is known.

Check the Home Assistant Telegram web page (https://home-assistant.io/integrations/telegram) for the limitations of whom Telegram can message. 

Now I'd recommend that you store your **API key** and your **ID** in your ```secret.yaml``` file. I've used dummy values for obvious reasons, but if you'd like a video on the ```secrets.yaml``` file and how to use it then let me know in the comments below.

Now let's **restart** Home Assistant.

Navigate to **Developer Tools**. Check your configuration. Press **Restart**. Confirm **Restart** and again now let's wait for Home Assistant to come back.

Now let's send a message to our Telegram Bot (here ```HomeAssistantX_bot```). Select **Services**. Search for and select ```Telegram bot: Send message``` and select. 

Now this has been vastly improved in recent revisions of Home Assistance so the old method of having to code a message has gone and it's now much more like the way to send notifications to Home Assistant companion app.

So let's give it a message and send it.

Type in a message (e.g. ```Hello from Home Assistant```), optionally give it a title (e.g. ```Home Assistant Message``). 

Now press **Call Service**.

The message will appear in the telegram chat window that you started likewise you can call this service from your automations as you would with sending notification messages you can also send photos videos sound Clips to your telegram all with no size limitations a put in the link description to everything talked about to help with your simple installation so there you have it a way of sending messages to yourself via the telegraph app and also to be able to send messages to the telegram app independently of having home assistant app there is a lot more that you can do with telegram integration and we have only skimmed the surface read through the documentation for yourself and if you'd like a dedicated Deep dive video on Telegram then let me know in the comments below enjoy sending those telegram messages until the next one
