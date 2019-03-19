---?image=assets/img/logo/slackbot-logo.jpg&size=90%

@title[Banner]
@box[message-box text-yellow text-20 fragment](Using Slackbot in our Daily Workflow)

---
@title[Introduction]
#### Based off **Takanori Suzuki's**
*Automate the Boring Stuff with Slackbot*
#### PyCon APAC 2019 talk

![Takanori Suzuki](assets/img/takanory.jpg)

---
@title[What We'll learn]

@snap[north-west text-center span-50]
#### We can integrate
@snapend

@snap[center span-50]
@img[span-50 fragment](assets/img/logo/slack-logo.png)
@snapend

@snap[north-east span-50]
@img[span-35 fragment](assets/img/logo/jira-logo.png)
@snapend

@snap[east span-50]
@img[span-35 fragment](assets/img/logo/python-logo.png)
@snapend

@snap[south-east span-50]
@img[span-35 fragment](assets/img/logo/shebang-logo.png)
@snapend

---
@title[Creating Slack Apps]

## Let's create a Slack App!

+++

@title[Slack API Dashboard]
@snap[north]
#### This is your app dashboard
<br />
@snapend

@snap[west span-35 text-right]
@img[span-60](https://puu.sh/D1yjy/790b023b66.png)
@snapend

@snap[east span-55 text-left]
@img[span-80](https://puu.sh/D1vRL/66ea9878e9.png)
@snapend

@snap[south]
See: [Building Slack apps](https://api.slack.com/slack-apps)
@snapend

+++

@title[Tokens and .ENV File]
Save your app credentials, for example, in a *.env* file. <br />
In Python, I used the module [python_dotenv](https://github.com/theskumar/python-dotenv) to load these like so:

```Bash
# .env
CLIENT_ID='XXXXXXXXXXX.XXXXXXXXXXXX'
CLIENT_SECRET='XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
VERIFICATION_TOKEN='XXXXXXXXXXXXXXXXXXXXXXXX'
```
```Python
# settings.py
from dotenv import load_dotenv
load_dotenv()
```
```Bash
# file structure
.
├── .env
└── settings.py
```

+++
@title[Incoming Webhooks Intro]
#### Activate Incoming Webhooks for your app
@img[center span-60](https://puu.sh/D1xTn/b301770221.png)

See: [Incoming Webhooks](https://api.slack.com/incoming-webhooks)

+++
@title[Webhook URL]
#### Authorize the App and choose the Channel
@img[span-35](https://puu.sh/D1xZX/958aca4ec9.png)

#### You will be given a **unique Webhook URL** *per channel*
```Bash
# Sample webhook URL:
https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
```

+++
@title[Sample POST Request]
Sample POST Request using Python
```Python
# sample_webhook.py
import json
import requests

data = json.dumps({'text': 'Ahoy from Python!'})

URL = (
    "https://hooks.slack.com"
    "/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX"
)

requests.post(URL, data=data)
```
```Bash
(venv) $ python sample_webhook.py
```
@img[center span-50](https://puu.sh/D1ybm/da5515bfb4.png)

---
@title[Creating Slackbots]

## Let's Create a Bot for our Slack App!

+++
@title[Overview]
@snap[north]
## Overview
@snapend

@ul
- Enable bots for our app.
- Create a Bot, which generates an OAth token.
- Use Python so that our bot can @color[darkblue](*listen_to*) and @color[darkblue](*respond_to*) messages from Slack.
- Install our App to our Workspace
- Invite the Bot to a channel where it can respond to.
@ulend

+++
@title[Bot File Structure]

@snap[north]
#### We need a few files for our bot to work
@snapend

```Bash
# File structure for our bot

ig_databot/
├── venv/  # Virtual Environment
├── ig_databot/plugins/
│   ├── __init__.py # empty file
│   └── ig_databot.py
├── run.py
└── slackbot_settings.py
```

+++
@title[Bot User]
This is our Bot User's settings.
@img[center span-60](https://puu.sh/D1DPe/03cce07104.png)

We can give it a custom name and an @handle so it's easy to call.
Tick @color[darkblue](*Always Show my Bot as Online*), too.

+++
@title[OAuth Token and Settings]
We need the *Bot User OAth Access Token* and save it to the **slackbot_settings.py** file

@img[center span-60](https://puu.sh/D1Epy/2d46cd61c5.png)

```Python
# slackbot_settings.py
API_TOKEN = 'xoxb-XXXXXXXXXXX-XXXXXXXXXXXX-XXXXXXXXXXXXXXXXXXXXXXXX'
PLUGINS = ['plugins.ig_databot']
```

+++
@[Run dot Py]
We will have this script run in the background for our slackbot to work.
We can also have this installed as a service.
```Python
# run.py
from slackbot.bot import Bot


def main():
    dataBot = Bot()
    dataBot.run()


if __name__ == "__main__":
    main()
```
```Bash
(venv) $ python ig_databot/run.py
```

+++
@title[Slackbot module and settings]
@snap[north]
Using Python's [slackbot module](https://github.com/lins05/slackbot):
@snapend

```Python
from slackbot.bot import listen_to, respond_to, default_reply
import re
import requests


@default_reply
def my_default_handler(message):
    message.reply('I currently have no response for that. Yet.')


@listen_to('help', re.IGNORECASE)
def hand_shake(message):
    message.reply('Reporting for duty.')


@respond_to('Hello', re.IGNORECASE)
def wazzaa(message):
    message.reply('Wazzaa!')
```

+++
@title[Listen/Respond To]

@snap[north span-100]
@box[bg-blue text-yellow smaller-text rounded](Default Reply#Besides specifying DEFAULT_REPLY in slackbot_settings.py, you can also decorate a function with the @color[darkblue](default_reply) decorator to make it the default reply handler, which is more handy.)
<br/>
@box[bg-blue text-yellow smaller-text rounded](Respond To#@color[darkblue](*respond_to*) is called when a message matching the pattern is sent to the bot (direct message or @botname in a channel/private channel chat))
<br/>
@box[bg-blue text-yellow smaller-text rounded](Listen To#@color[darkblue](*listen_to*) is called when a message matching the pattern is sent on a channel/private channel chat (not directly sent to the bot))
@snapend

+++
@title[Install to Workspace]
In Slack, browse the  **Apps** then click Install when we find the app we created.

@img[center span-50](https://puu.sh/D1F4V/790902f4a1.png)

Then, let's invite our bot to a channel.
@img[center span-50](https://puu.sh/D1F8A/2144761f88.png)

+++
@title[Test Messages]

Let's test our bot:

@img[center span-50](https://puu.sh/D24or/826743188f.png)

+++
@title[Attachments]

It also supports message attachments:
```Python
@respond_to('status', re.IGNORECASE)
def status(message):
    fields = [
        {"title": "Date:", "value": "", "short": True}, {"title": "Status:", "value": "", "short": True},
        {"title": "", "value": "2019-03-18 00:52:11", "short": True}, {"title": "", "value": "Start parser for Argentina", "short": True},
    ]
    attachment = json.dumps([
        {
            "fallback": "Data Parser Status",
            "title": "Data Parser Status",
            "text": """Running log as of {}\n\n""".format(current_date)),
            "color": "#004492",
            "fields": fields
        }
    ])
    message.send_webapi('', attachments)
```
@img[center span-50](https://puu.sh/D25k8/4eece403d2.png)


---?image=assets/img/presenter.jpg

@snap[north span-100 headline]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
