---
layout: post
author: Abwao
---
[Rasa](https://rasa.com/){:target="_blank"} is an [open source](https://opensource.com/resources/what-open-source){:target="_blank"} software package with user friendly tools to design, train and build contextual artificial intelligence chatbots.

### Prerequisites
- You'll need to have some experience with **Python**; at least how to install it and how to install packages with **pip**.
- For **Windows** users, you'll need to ensure Microsoft VC++ Compiler is installed. Please see [Windows Prerequisites](https://rasa.com/docs/rasa/user-guide/installation/#windows-prerequisites).

### Installation
This simple [getting started guide](https://rasa.com/docs/getting-started/) will see you through installation, and even create a sample Rasa project that you can try out right away. I'd recommend going through the [Rasa Tutorial](https://rasa.com/docs/rasa/user-guide/rasa-tutorial/), and working in a new folder. 

### Editing the Files
Now comes the tricky part - giving the chatbot a brain and a personality.

First the brains. The chatbot understands a user's input by learning the various *intents* and *entities* in the **nlu.md** file, which is in the **data** directory/folder. Please see [Training Data Format](https://rasa.com/docs/rasa/nlu/training-data-format/). You can add as many *intents* as you wish - just be careful to make their respective examples distinct so that the chatbot doesn't get mixed up. 

The *stories* in **stories.md** give the chatbot sample conversation flows, so that it can learn how natural conversations would go. Please see [Stories](https://rasa.com/docs/rasa/core/stories/). [Slots](https://rasa.com/docs/rasa/core/slots/) and [Forms](https://rasa.com/docs/rasa/core/forms/) are the chatbots memory.

The *domain* file - **domain.yml** - is like the body of the chatbot (brains, limbs, mouth and all). It specifies the *intents* & *entities* the bot should know; the *slots* and *forms* it should store, the *actions* it can take and the *templates* (things it can say). Please see [Domains](https://rasa.com/docs/rasa/core/domains/).

For twe adjustments to the **endpoints.yml**, **config.yml**, **credentials.yml**, and **actions.py** files, I'd recommend taking some time to go through the [Rasa Docs](https://rasa.com/docs/rasa/). They're really good and well detailed. It's the best way to find out exactly what's happening behind the scenes, and how you can mould the chatbot in line with how you envisioned it. 

**Disclaimer:** some features *might* at times prove quite challenging to design and implement (custom actions are particularly notorious), but you *will* find plenty of help in online forums. Happy coding 🙂️.

If you'd like, you can download a sample chatbot that I'd worked on [here](https://github.com/Tim-Abwao/rasa-chatbot).
