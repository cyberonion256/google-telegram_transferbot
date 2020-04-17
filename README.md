# google-telegram_transferbot
This Google Apps Script links a Telegram bot to a google spreadsheet and allows command-based information storaging

Features:
- Feed a Telegram bot with information to store in Google Spreadsheet
- Currently set to store URLs and enter keywords, locations, persons, comments - but: Fully customizable to store any information
- Indicate type of stored information with Telegram commands (starting with '/'), e.g. keywords, persons, locations
- Stores URLs as HTML in Google Drive folder
- Prevents input confusion between two users by blocking the input as long as another user is still requesting the bot
- Easy to install, free of charge, 24/7 readiness

# 1. Initizalization

>> Set up follows this YouTube tutorial: https://www.youtube.com/watch?v=mKSXd_od4Lg <<

- Set up a telegram bot with @BotFather (relevant information: bot token
- Set up new Google Spreadsheet (relevant information: webApp url, Spreadsheet id)
- Set up Google Drive folder to store URLs (relevant information: folder id)

# 2. Prepare Google Spread Sheet

The bot is prepared to fill a prepared spread sheet. The provided template consistes of three worksheets:
- Worksheet 1 "collection": This is where the finished input is stored; the columns must match those of Worksheet 2 "assembler".
- Worksheet 2 "assembler": This is where the bot assembles a current input before it is pushed to the collection or deleted; the columns must match those of Worksheet 1 "collection".
- Worksheet 3 "command_storage": This is a temporary storage for command into to correctly refer following input to the correct collumns, e.g. if the command is '/person_add', the next entries are added in the person column in the "assembler" sheet.

Suggestion: Import the spreadsheet, see how the bot works and customize the bot to your needs afterwards.
