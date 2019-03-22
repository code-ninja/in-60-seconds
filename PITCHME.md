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
@title[What We'll Learn]

@snap[north text-center center]
#### Today, we will learn how integrate
@snapend

@snap[west span-50 text-center]
@img[span-50 fragment](assets/img/logo/slack-logo.png)
@snapend

@snap[east span-50 text-center]
@img[span-50 fragment](assets/img/logo/python-logo.png)
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

```Shell
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

```Shell
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


---?image=assets/img/presenter.jpg

@snap[north span-100 headline]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
