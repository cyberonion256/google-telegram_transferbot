# Google-Telegram transfer bot
This Google Apps Script links a Telegram bot to a google spreadsheet and allows command-based information storaging

## Features:
- **Link Telegram to Google Spreadsheet:** Feed a Telegram bot with information to store in Google Spreadsheet
- **Fill in customizable columns:** Currently set to digest a URL and enter keywords, locations, persons, comments linked to the URL - but: Fully customizable to store any information
- **Telegram command based**: Indicate type of stored information with Telegram commands (starting with '/'), e.g. keywords, persons, locations
- **Back up for URLs**: Stores URLs as HTML in Google Drive folder
- **Single Input**: Prevents input confusion between two users by blocking the input as long as another user is still requesting the bot
- **Simple syntax**: The core element of the bot relies only on if-else statements and is understandable also to programming beginners
- **Easy to install, free of charge, 24/7 readiness**

## 1. Initizalization

- Set up a telegram bot with @BotFather (relevant information: bot token), see here: https://core.telegram.org/bots
- Set up new Google Spreadsheet (relevant information: webApp url, Spreadsheet id)
- Set up Google Drive folder to store URLs (relevant information: folder id)

>> Set up follows this YouTube tutorial: https://www.youtube.com/watch?v=mKSXd_od4Lg 

## 2. Prepare Google Spread Sheet

The bot in its current specification is written to fill the attached spread sheet [Template](docs/Spreadsheet_template_transferbot.xls). The provided template consistes of three worksheets:
- *Worksheet 1 "collection":* This is where the finished input is stored; the columns must match those of Worksheet 2 "assembler".
- *Worksheet 2 "assembler":* This is where the bot assembles a current input before it is pushed to the collection or deleted; the columns must match those of Worksheet 1 "collection".
- *Worksheet 3 "command_storage":* This is a temporary storage for command into to correctly refer following input to the correct collumns, e.g. if the command is '/person_add', the next entries are added in the person column in the "assembler" sheet.

*Suggestion*: Import the spreadsheet, see how the bot works and customize the bot to your needs afterwards.

## Import and fill individual details to Google Apps Script code

The bot runs on a Google Web App, using Google Apps script - a JavaScript based programming. To get the bot running, you can download the .js (JavaScript) files, rename them to .gs (Google Apps Script) and import them to your Google Script Apps project.

To connect the script to your bot and Google spreadsheet, you have to subsitute the following variable:
- **Telegram bot token**: you will receive the token from the Telegram botfather (looks like this: 1175871460:AAGDapaqpOGdYgsMqDL0lP213IKlMiqXGog)
- **Google webAppUrl**: you will receive the webAppUrl when you publish your script for the first time as WebApp (looks like this: https://script.google.com/macros/s/AKfydbw7KIMKGdLNpmPtdXJoQF7Row61ItJq8Dztvjh9CNNXZ1EmJio/exec)
- **Google Spreadsheet id**: you fill find the ss_id in the URL of your spreadsheet (looks like this: "1Bsn7gZX5jZ_lTVucM5ebaDzmxtok3UtMNVUb8021h3e")
- **Telegram admin id**: if you want to receive status updates for your bot, please fill in your Telegram id (or the one of the admin). You'll find the id if you send your bot a message and look it up in the as sender_id... ;-) (looks like this: 325208322)
- Telegram commands: Telegram commands start with a forward slash ('/') and are fully customizable. In the inital setting, we have specified the following 10 commands that the bot reacts to: /start_input, /url_add, /key_add, /place_add, /person_ad, /comment_add, /help, /cancel, /end_input, /start.

The script uses the following functions:
- getMe(): checking bot status
- setWebhook(): setting telegram webhook (to connect Google WebApp to bot)
- deleteWebhook(): deleting telegram webhook
- **doPost()**: interaction with bot (digest messages to bot and post reponses) --> this is the core of your bot!
- getHTMLfromURL(url): grab HTML from given URL, returns html
- StoreHtmlToDrive(html_input, file_title): stores HTML to Google Drive folder, set with folder_id
- isolateURL(string): isolates urls starting with HTTP and HTTPS from strings
- three send functions for replies of the telegram bot to its users

## Prepare Telegram bot

As a last step, add the commands to your telegram bots via the BotFather (https://core.telegram.org/bots#commands). To use the preset functions of the transfer bot, add the following commands to 

```
start_input - Start sending information 
url_add - Add URL (only one)
key_add - Add Keyword (multiple)
place_add - Add Place, City, or Country (multiple)
person_add - Add Person (multiple)
comment_add - Add comment (only one)
help - Get some help
cancel - Cancel process and delete input
end_input - End Input
```

Watch out: The bot does not work with inline commands!

## Start off = customize to your own needs

Take a closer look at the doPost() function, as it stores the "heart" of the transfer bot. With little programming skills, you can start adapting the transfer bot to your own needs. Make sure to always select the appropriate cells in the Spreadsheet as it works as your temporary (Worksheet 2 + 3) and permanent storage. 

Have fun!
