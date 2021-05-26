
# Youtube Audio Downloader Bot  
[![enter image description here](https://img.shields.io/badge/Bot-@ytadlbot-blue?logo=telegram&style=for-the-badge)](https://t.me/ytadlbot)
![GitHub deployments](https://img.shields.io/github/deployments/tanveerraza789/ytadlbot/ytadlbot?label=heroku&logo=heroku&style=for-the-badge)

A Telegram bot written in python that downloads music from YouTube and send it into the chat.  
  
## Working  
The bot filter out all the YouTube urls from the received message and send the downloaded audio back to the user.  
  
## Detailed working
1. Program gathers environment variables : BOT_TOKEN, HEROKU_APP_NAME, POOLING, AUDIO_DB, USER_DB, OPEN_CHANNEL_USERNAME   
2. Program initializes logger and db-manager  
   - Logger logs the user and number of commands they execute  
   - db-manager is used to manage links and message id of the uploaded file on the open channel  
      
3. Bot is fired up using the api token  
4. Command handles are provided to the bot updater object  
5. checks if POLLING is enabled  
   - if pooling is enabled, starts polling  
   - if not then start web hook  
      
6. Listens for updates  
   1. If update contains a command then executes it as provided  
   2. If no command is specified, the bot tries to extract YouTube URLs from the text provided  
   3. Tried to extract links if playlist is provided  
   4. Downloads M4A file from all the links gathered from previous step  
   5. Logs user activity for downloading each file  
   6. For each URL, checks the audio db for its existence if open channel is provided  
       - If already available, then forward it to the user   
       - Else download and add it to the db  
   7. If no open channel is provided, simply send it to the user  
   8. Process is completed, wait for another job  
   9. If the program is terminated  
       1. Stop the bot  
       2. Close connections from both the DB  
       3. Exit  
  
  
## Requirements  
1. [Pafy](https://pythonhosted.org/Pafy/)  
2. [python-telegram-bot](https://python-telegram-bot.org/)  
3. [music-tag](https://github.com/KristoforMaynard/music-tag)  
4. urlextract  
5. requests  
6. hashlib  
7. [psycopg2](https://www.psycopg.org/)  
  
## Deploy the bot  
Create a bot on telegram using [@botfather](t.me/botfather)    
Create an app on [heroku](https://dashboard.heroku.com/)   
Create a public channel on telegram  
Set environment variables in heroku app  
- BOT_TOKEN = your bot API token  
- HEROKU_APP_NAME = name of your heroku app  
- POOLING : if you're running this on your local machine, please set POOLING = True else leave this if you're deploying on heroku  
- AUDIO_DB : PostgreSQL DB link for audio management  
- USER_DB : PostgreSQL DB link for user management  
- OPEN_CHANNEL_USERNAME : Universal upload channel username, bot will upload files here and forward it to the user  
  
Deploy the bot [read here](https://devcenter.heroku.com/articles/getting-started-with-python)  
  
## Future plans  
1. Making a desktop application that can be used by everyone on their machine by providing their bot API token