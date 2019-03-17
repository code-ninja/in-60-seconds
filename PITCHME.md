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

---?color=#E58537
@title[Add A Little Imagination]

@snap[north-west]
#### Add a splash of @color[cyan](**color**) and you are ready to start presenting...
@snapend

```Python
from slackbot.bot import listen_to, respond_to, default_reply
import re
import requests


@default_reply
def my_default_handler(message):
    message.reply('I currently have no response for that. Yet.')
```

---?image=assets/img/presenter.jpg

@snap[north span-100 headline]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
