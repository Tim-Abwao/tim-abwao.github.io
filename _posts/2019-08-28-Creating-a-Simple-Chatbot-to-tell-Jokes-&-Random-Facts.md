---
layout: post
author: Abwao
---

[Rasa](https://rasa.com/){:target="_blank"} is an [open source](https://opensource.com/resources/what-open-source){:target="_blank"} software with user-friendly tools to design, train and build intelligent chatbots.

### Installation
This simple [getting started guide](https://rasa.com/docs/getting-started/) will take you through the installation process, and even create a chatbot (Rasa project) that you can try out right away. The [Rasa Tutorial](https://rasa.com/docs/rasa/user-guide/rasa-tutorial/) is the best way to get acquainted with how Rasa works. 


**Note:** Please check out the [Installation guide](https://rasa.com/docs/rasa/user-guide/installation/#installation-guide) for platform-specific dependencies (e.g. if you're using **Windows**, you'll need to have the Microsoft VC++ Compiler installed beforehand, or else the Rasa installation will fail).

### Modifying the Chatbot
You can give the chatbot a unique personality by editing the files in the Rasa Project.

First the brains: The chatbot is 'taught' using training data in the **data** directory/folder. It understands a user's input by 'learning' the various *intents* and *entities* in the **nlu.md** file (Please see [Training Data Format](https://rasa.com/docs/rasa/nlu/training-data-format/)). 

You can add as many *intents* as you wish to customise it (e.g. for small talk, customer service, ticket-booking, financial-assistant service, etc) - just be careful to make sure the intents' respective examples are distinct, so that the chatbot doesn't mix them up.

The *stories* in the **stories.md** file present the chatbot with sample conversation flows, teaching it how real-world conversations would go, and helping it predict the most approprite responses (Please see [Stories](https://rasa.com/docs/rasa/core/stories/)).

The body/skelleton of the chatbot is the *domain* file - **domain.yml**. It assembles all the *intents* & *entities* the chatbot should know, the *slots* and *forms* it should store, the *actions* it can take and the *templates* (things it can say). Please see [Domains](https://rasa.com/docs/rasa/core/domains/), [Slots](https://rasa.com/docs/rasa/core/slots/) and [Forms](https://rasa.com/docs/rasa/core/forms/). 

For adjustments to the **endpoints.yml**, **config.yml**, **credentials.yml**, **actions.py** and any other files, I'd recommend taking some time to go through the [Rasa Docs](https://rasa.com/docs/rasa/). They're really good, and well detailed. It's the best way to find out exactly what's happening behind the scenes, and discover how to mould the chatbot in line with how you envisioned it. 

**Hint:** some features *might* at times appear quite challenging to design and implement (custom actions are particularly notorious), but you *will* find plenty of help in online forums.

If you'd like, you can download a sample chatbot I had made [here](https://github.com/Tim-Abwao/rasa-chatbot). It uses internet APIs to tell jokes and random number/date facts. I'll re-edit this page in future to describe how to build it.
