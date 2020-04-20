---
layout: post
author: Abwao
last_modified_at: 2020-03-17T15:18:32+03:00
---

[Rasa](https://rasa.com/) is an [open source](https://opensource.com/resources/what-open-source) Python package with easy-to-use tools for building intelligent text and voice based chatbots. It features several *machine learning*, *natural language processing* and *natural language understanding* tools to produce smart, life-like chatbots.

## Installation
Please check out the [step-by-step installation guide](https://rasa.com/docs/rasa/user-guide/installation/#installation-guide) for platform-specific instructions. This [getting started guide](https://rasa.com/docs/getting-started/) installs Rasa and creates a basic chatbot (Rasa project) that you can try out right away. 

## Getting Started
The [Rasa Tutorial](https://rasa.com/docs/rasa/user-guide/rasa-tutorial/) is the best way to get acquainted with how Rasa works. It defines the fundamental files required to build chatbots, and their varied formats. 

## Anatomy of the Chatbot
### (i). 'The brains'
The chatbot is taught/trained using data in the **data** folder. It understands a user's input by learning the various *intents* and *entities* in the **nlu.md** file (Please see [Training Data Format](https://rasa.com/docs/rasa/nlu/training-data-format/)). 

You can add as many *intents* as you wish to customise it (e.g. for small talk, customer service, ticket-booking, financial-assistant service, etc). Just be careful to make sure the intents' respective examples are distinct, and unlikely to be mixed up.

The [stories](https://rasa.com/docs/rasa/core/stories/) in the **stories.md** file present the chatbot with sample real-world conversation flows to help it predict the most approprite responses.

### (ii). 'The body'
The skeleton of the chatbot is the [domain](https://rasa.com/docs/rasa/core/domains/) in the **domain.yml** file. It holds all the *intents* & *entities* the chatbot should know, the [slots](https://rasa.com/docs/rasa/core/slots/) and [forms](https://rasa.com/docs/rasa/core/forms/) it should store, the list of [actions](https://rasa.com/docs/rasa/core/actions/) it can perform, the [responses](https://rasa.com/docs/rasa/core/responses/) it can make  and additional configurations. 

The **credentials.yml** file has the details for connections to channels other than the command line, e.g. Telegram & Facebook Messenger.

The **config.yml** file defines the [pipeline](https://rasa.com/docs/rasa/nlu/choosing-a-pipeline/) and [policies](https://rasa.com/docs/rasa/core/policies/) to use to train the chatbot.

The **endpoints.yml** file contains authorisation details for connections to external services e.g. MongoDB or PostgreSQL databases.

The **actions.py** file contains [custom actions](https://rasa.com/docs/rasa/core/actions/#id7) written in Python. 

**Hint:** some features *might* at times appear quite challenging to design and implement (complex custom actions are particularly notorious), but you *will* find plenty of help in the [Rasa community](https://forum.rasa.com/) and other online forums.

## Next Steps
It's recommended to go through the official [Rasa Docs](https://rasa.com/docs/rasa/), as they're the most detailed and up-to-date way of finding out exactly what's happening behind the scenes, and how to mould your chatbot in line with how you envisioned it.

If you'd like, you can download and try out a sample chatbot [here](https://github.com/Tim-Abwao/rasa-chatbot). It can tell jokes and random number/date facts, which it collects from online APIs.