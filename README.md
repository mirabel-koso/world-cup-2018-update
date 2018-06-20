# Slackbot Russia 2018 World Cup

A bot for slack to message about matches of the 2018 FIFA World Cup and other custom actions

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Modules (NEW!)
Now you can develop your own modules to make the bot do other things based on actions. The football-data is now a module, so starting the app must include the module. As an example there is another module that parses the web www.coperos.com for a rooster and post the rooster to the channel. To launch the new module the command is (node index.js coperos).
For example you can run the football-data every 10 minutes, the instagram every 30 minutes and the coperos once a day at 23:00:
```
CRON_SCHEDULE="*/10 * * * *" node index.js football-data
INSTA_ACCOUNT=maradona INSTA_FILTER="Copa del Mundo 2018" CRON_SCHEDULE="*/30 * * * *" node index.js instagram-pic
CRON_SCHEDULE="0 23 * * *" node index.js coperos
```

## What you have to do
- Configure the slack webhook https://api.slack.com/incoming-webhooks
- Run the app somewhere (node index.js football-data)

### Football-data module extra
- Get an api token from https://api.football-data.org/client/register

## What it does for you

### Football-data module
- Post every day, the matches of the day
- Updates for new goals on each match
- Highlight your preferred team
- Supports multiple languages
- Supports multiple timezones
- Uses flag emoticons

### Coperos module
- Scrapes the www.coperos.com/torneos/your-tourament url
- Post the current rooster extracted from the site

## Configs
All configurations can be modified by environmental variables, or using the .env file. Here are the different configurations available:

### General
- LOG_LEVEL - type: string, default `"info"`, The log level to the console (error, info, debug, silly, etc...)
- LANGUAGE - type: string, default: `"en"`, Language for the translations, the "es" language is already included, any new language should be added as a new file in the locales folder following the convention of the other files already there.
- CRON_SCHEDULE, type: string (cron expression), default: `"*/15 * * * *"`, The cron expression to schedule each Api check, see https://es.wikipedia.org/wiki/Cron_(Unix)
- SLACK_ENABLED, type: boolean, default: `true`, Enable or disable the post to slack, good for testing the configuration.
- SLACK_CHANNEL, type: string, default: `"#worldcup"`, The name of the slack channel that the bot will post to.
- SLACK_BOT, type: string, default: `"Worldcup"`, The name of the bot (configured in slack) that will make the post.
- SLACK_WEBHOOK, type string, default: `"https://hooks.slack.com/services/***`, The slack webhook url, the default will not work, you need to get this from slack when creating the webhook.
- ENABLE_STATIC_WEB, type boolean, default: `false`, Enable a static web server that serves logs, helpful for heroku, enabled in the heroku app by default.
