![alt text](https://github.com/zerocurrencycoin/Zero-Telegram-Discord-Relay-Bot/blob/master/Mr%20Bender%20Zero%20small.png)


Zero - Mr Bender Bot 
=========
Zero - Mr Bender Bot is a bot which bridges chat from [Zero's Telegram](https://t.me/zerocurrency) with #General-Chat in [Zero's Discord](https://discord.gg/Jq5knn5) 

Any chat from these channels will be relayed instantly.


Features & known bugs
---------------------

The bot is able to relay text messages and media files between Discord and Telegram. @-mentions, URLs, code (both inline and block-style) works well

For a list of known bugs, or to submit a bug or feature request, see this repo's "Issues" tab


Step by step installation:
--------------------------
Setting up the bot requires basic knowledge of the command line, which is bash or similar on Linux/Mac, and cmd.exe in Windows

 1. Install [nodejs](https://nodejs.org)
 2. Clone this git repo, or download it as a zip or whatever
 3. Open a terminal and enter the repo with the [`cd`](https://en.wikipedia.org/wiki/Cd_(command)) command. Something like `cd Downloads/TediCross-master`. Your exact command may differ
 4. Run the command `npm install`
 5. Make a copy of the file `example.settings.yaml` and name it `settings.yaml`
 6. Aquire a bot token for Telegram ([How to create a Telegram bot](https://core.telegram.org/bots#3-how-do-i-create-a-bot)) and put it in the settings file
   - The Telegram bot must be able to access all messages. Talk to [@BotFather](https://t.me/BotFather) to disable privacy mode for the bot
   - Do NOT use another bot you already have running. That will cause all sorts of weird problems. Make a new one
 7. Aquire a bot token for Discord ([How to create a Discord bot](https://github.com/reactiflux/discord-irc/wiki/Creating-a-discord-bot-&-getting-a-token)) and put it in the settings file under `discord.token`. **NOTE** that the token is NOT the "Client Secret". The token is under the section "App bot user" further down the page
   - Do NOT use another bot you already have running. That will cause all sorts of weird problems. Make a new one
 8. Add the Telegram bot to the Telegram chat
   - If the Telegram chat is a supergroup, the bot also needs to be admin of the group, or it won't get the messages. The creator of the supergroup is able to give it admin rights
 9. Add the Discord bot to the Discord server (https://discordapp.com/oauth2/authorize?client_id=YOUR_CLIENT_ID_HERE&scope=bot&permissions=248832). This requires that you have admin rights on the server
 10. Start TediCross: `npm start`
 11. Ask the bots for the remaining details. In the Telegram chat and the Discord channel, write `/chatinfo`. Put the info you get in the settings file.
   - If you want to bridge a Telegram group or channel, remember that the ID is negative. Include the `-` when entering it into the settings file
   - It is important that the Discord IDs are wrapped with single quotes when entered into the settings file. `'244791815503347712'`, not `244791815503347712`
 12. Restart TediCross. You stop it by pressing CTRL + C in the terminal it is running in

Done! You now have a nice bridge between a Telegram chat and a Discord channel


Settings
--------

As mentioned in the step by step installation guide, there is a settings file. Here is a description of what the settings do.

* `telegram`: Object authorizing and defining the Telegram bot's behaviour
	* `token`: The Telegram bot's token. It is needed for the bot to authenticate to the Telegram servers and be able to send and receive messages. If set to `"env"`, TediCross will read the token from the environment variable `TELEGRAM_BOT_TOKEN`
	* `useFirstNameInsteadOfUsername`: **EXPERIMENTAL** If set to `false`, the messages sent to Discord will be tagged with the sender's username. If set to `true`, the messages sent to Discord will be tagged with the sender's first name (or nickname). Note that Discord users can't @-mention Telegram users by their first name. Defaults to `false`
	* `colonAfterSenderName`: Whether or not to put a colon after the name of the sender in messages from Discord to Telegram. If true, the name is displayed `Name:`. If false, it is displayed `Name`. Defaults to false
	* `skipOldMessages`: Whether or not to skip through all previous messages cached from the telegram-side and start processing new messages ONLY. Defaults to true. Note that there is no guarantee the old messages will arrive at Discord in order
	* `sendEmojisWithStickers`: Whether or not to send the corresponding emoji when relaying stickers to Discord
* `discord`: Object authorizing and defining the Discord bot's behaviour
	* `token`: The Discord bot's token. It is needed for the bot to authenticate to the Discord servers and be able to send and receive messages. If set to `"env"`, TediCross will read the token from the environment variable `DISCORD_BOT_TOKEN`
	* `skipOldMessages`: Whether or not to skip through all previous messages sent since the bot was last turned off and start processing new messages ONLY. Defaults to true. Note that there is no guarantee the old messages will arrive at Telegram in order. **NOTE:** [Telegram has a limit](https://core.telegram.org/bots/faq#my-bot-is-hitting-limits-how-do-i-avoid-this) on how quickly a bot can send messages. If there is a big backlog, this will cause problems
	* `useNickname`: Uses the sending user's nickname instead of username when relaying messages to Telegram
* `debug`: If set to `true`, activates debugging output from the bot. Defaults to `false`
* `bridges`: An array containing all your chats and channels. For each object in this array, you should have the following properties:
	* `name`: A internal name of the chat. Appears in the log
	* `direction`: Direction of the bridge. "both" for bidirectional, "d2t" for discord-to-telegram, "t2d" for telegram-to-discord
	* `telegram.chatId`: ID of the chat that is the Telegram end of this bridge. See step 11 on how to aquire it
	* `telegram.relayJoinMessages`: Whether or not to relay messages to Discord about people joining the Telegram chat
	* `telegram.relayLeaveMessages`: Whether or not to relay messages to Discord about people leaving the Telegram chat
	* `discord.guild`: ID of the server the Discord end of the bridge is in. If a message to the bot originates from within this server, but not the correct channel, it is ignored, instead of triggering a reply telling the sender to get their own bot. See step 11 on how to aquire it
	* `discord.channel`: ID of the channel the Discord end of the bridge is in. See step 11 on how to aquire it
	* `discord.relayJoinMessages`: Whether or not to relay messages to Telegram about people joining the Discord chat
	* `discord.relayLeaveMessages`: Whether or not to relay messages to Telegram about people leaving the Discord chat

The available settings will occasionally change. The bot takes care of this automatically


Want to donate?
---------------

* ZER: t1cDotxmVEJrniDjNqqjsCWq8mLMApV8vXC

