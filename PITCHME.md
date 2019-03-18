---?image=assets/img/logo/slackbot-logo.jpg&size=90%

@box[message-box text-yellow text-20 fragment](Using Slackbot in our Daily Workflow)

---

#### Based off **Takanori Suzuki's**
*Automate the Boring Stuff with Slackbot*
#### PyCon APAC 2019 talk

![Takanori Suzuki](assets/img/takanory.jpg)

---
@title[Discussion]

@snap[north-west text-center span-50]
#### We will learn how to integrate
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

## Creating Slack Apps

+++
#### This is your app dashboard

@snap[west span-40]
@img[](https://puu.sh/D1yjy/790b023b66.png)
@snapend

@snap[east span-50]
@img[](https://puu.sh/D1ygM/d2617ab492.png)
@snapend

See: [Building Slack apps](https://api.slack.com/slack-apps)

+++

@snap[west span-50]
@img[Sidebar](https://puu.sh/D1yjy/790b023b66.png)
@snapend

@snap[east span-50]
@img[](https://puu.sh/D1vRL/66ea9878e9.png)
@snapend

+++

#### Save your app credentials, for example, in a *.env* file
In Python, I used the module [python_dotenv](https://github.com/theskumar/python-dotenv) to load these like so:
```text
.
├── .env
└── settings.py
```

```Python
# settings.py
from dotenv import load_dotenv
load_dotenv()
```

+++

#### Activate Incoming Webhooks for your app
@snap[center]
@img[](https://puu.sh/D1xTn/b301770221.png)
See: [Incoming Webhooks](https://api.slack.com/incoming-webhooks)
@snapend

+++

@snap[span-50]
@img[Authorize App and choose the Channel](https://puu.sh/D1xZX/958aca4ec9.png)
@snapend

#### You will be given a unique Webhook URL *per channel*
```Bash
# Sample webhook URL:
https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
```

+++

#### Sample POST Request using Python
```Python
import json
import requests

data = json.dumps({'text': 'Ahoy from Python!'})

URL = (
    "https://hooks.slack.com"
    "/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX"
)

    requests.post(URL, data=data)
```

@img[Post from Python](https://puu.sh/D1ybm/da5515bfb4.png)

---?image=assets/img/presenter.jpg

@snap[north span-100 headline]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
