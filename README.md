# Google-Telegram transfer bot
This Google Apps Script links a Telegram bot to a google spreadsheet and allows command-based information storaging

**Features:**
- Feed a Telegram bot with information to store in Google Spreadsheet
- Currently set to store URLs and enter keywords, locations, persons, comments - but: Fully customizable to store any information
- Indicate type of stored information with Telegram commands (starting with '/'), e.g. keywords, persons, locations
- Stores URLs as HTML in Google Drive folder
- Prevents input confusion between two users by blocking the input as long as another user is still requesting the bot
- Easy to install, free of charge, 24/7 readiness

## 1. Initizalization

>> Set up follows this YouTube tutorial: https://www.youtube.com/watch?v=mKSXd_od4Lg 

- Set up a telegram bot with @BotFather (relevant information: bot token)
- Set up new Google Spreadsheet (relevant information: webApp url, Spreadsheet id)
- Set up Google Drive folder to store URLs (relevant information: folder id)

## 2. Prepare Google Spread Sheet

The bot is prepared to fill a prepared spread sheet. The provided template consistes of three worksheets:
- *Worksheet 1 "collection":* This is where the finished input is stored; the columns must match those of Worksheet 2 "assembler".
- *Worksheet 2 "assembler":* This is where the bot assembles a current input before it is pushed to the collection or deleted; the columns must match those of Worksheet 1 "collection".
- *Worksheet 3 "command_storage":* This is a temporary storage for command into to correctly refer following input to the correct collumns, e.g. if the command is '/person_add', the next entries are added in the person column in the "assembler" sheet.

*Suggestion*: Import the spreadsheet, see how the bot works and customize the bot to your needs afterwards.

## Import and fill individual details to Google Apps Script code

The bot runs on a Google Web App, using Google Apps script - a JavaScript based programming. To get the bot running, you can import all .gs files into one script but I recommand you to keep it separated.

To connect the script to your bot and Google spreadsheet, you have to subsitute the following variable:
- **Telegram bot token**: you will receive the token from the Telegram botfather (looks like this: 1175871460:AAGDapaqpOGdYgsMqDL0lP213IKlMiqXGog)
- **Google webAppUrl**: you will receive the webAppUrl when you publish your script for the first time as WebApp (looks like this: https://script.google.com/macros/s/AKfydbw7KIMKGdLNpmPtdXJoQF7Row61ItJq8Dztvjh9CNNXZ1EmJio/exec)
- **Google Spreadsheet id**: you fill find the ss_id in the URL of your spreadsheet (looks like this: "1Bsn7gZX5jZ_lTVucM5ebaDzmxtok3UtMNVUb8021h3e")
- **Telegram admin id**: if you want to receive status updates for your bot, please fill in your Telegram id (or the one of the admin). You'll find the id if you send your bot a message and look it up in the as sender_id... ;-) (looks like this: 325208322)

The script uses the following functions:
- getMe(): checking bot status
- setWebhook(): setting telegram webhook (to connect Google WebApp to bot)
- deleteWebhook(): deleting telegram webhook
- **doPost()**: interaction with bot (digest messages to bot and post reponses) --> this is the core of your bot!
- getHTMLfromURL(url): grab HTML from given URL, returns html
- StoreHtmlToDrive(html_input, file_title): stores HTML to Google Drive folder, set with folder_id
- isolateURL(string): isolates urls starting with HTTP and HTTPS from strings
- three send functions for replies of the telegram bot to its users
