---
layout: post
author: Abwao
last_modified_at: 2020-05-27T23:46:00+03:00
---

[*Rasa*](https://rasa.com/) is an [open source](https://opensource.com/resources/what-open-source) Python package with easy-to-use tools for building intelligent text and voice based chatbots.

It features several *machine learning*, *natural language processing* and *natural language understanding* tools to produce smart, life-like chatbots.

## Installation

```bash
# Installing the Python development environment
$ sudo apt update
$ sudo apt install python3-dev python3-pip
# Creating a virtual environment
$ python3 -m venv env
$ source env/bin/activate
$ pip install -U pip
# Installing Rasa
$ pip install rasa
```

Please visit *Rasa's* [step-by-step installation guide](https://rasa.com/docs/rasa/user-guide/installation/#installation-guide) for help on how to install it in *macOS*, *Windows* or from source.

## Getting Started

The [*Rasa* Basics](https://rasa.com/docs/rasa/user-guide/rasa-tutorial/) tutorial demonstrates how to create an *assistant* (project), and introduces the necessary files and commands. If you're unfamiliar with *Rasa*, please take the time to go through it.

## Rasa Assistant to tell Jokes & Random Facts

### 1. Install Rasa

After installing *Rasa* (preferably in a virtual environment as shown above), initiate the project (assistant) to get the default files:

```bash
$ mkdir chatbot; cd chatbot
$ rasa init --no-prompt
```

### 2. Add Custom Actions

[Custom actions](https://rasa.com/docs/rasa/core/actions/#custom-actions) in *Rasa* are created as classes. They can be programmed to achieve specific desired outcomes

Below are 3 custom actions that fetch joke and fact content from APIs. Include them in the **actions.py** file:

```python
from typing import Any, Text, Dict, List
from rasa_sdk import Action, Tracker
from rasa_sdk.executor import CollectingDispatcher
from urllib.request import urlopen
from datetime import date
from ast import literal_eval


class ActionGetMathFact(Action):

    def name(self) -> Text:
        return "get_math_fact"

    def run(self, dispatcher: CollectingDispatcher, tracker: Tracker,
            domain: Dict[Text, Any]) -> List[Dict[Text, Any]]:
        # get message from numbersapi
        fact = urlopen('http://numbersapi.com/random/trivia').read()
        # send fact as message
        dispatcher.utter_message(fact.decode('utf-8'))
        return []


class ActionGetDateFact(Action):

    def name(self) -> Text:
        return "get_date_fact"

    def run(self, dispatcher: CollectingDispatcher, tracker: Tracker,
            domain: Dict[Text, Any]) -> List[Dict[Text, Any]]:
        # get day and month
        day = date.strftime(date.today(), '%m/%d')
        # get message from numbersapi
        day_fact = urlopen('http://numbersapi.com/' + day + '/date').read()
        # send fact as message
        dispatcher.utter_message(day_fact.decode('utf-8'))
        return []


class ActionGetJoke(Action):

    def name(self) -> Text:
        return "get_joke"

    def run(self, dispatcher: CollectingDispatcher, tracker: Tracker,
            domain: Dict[Text, Any]) -> List[Dict[Text, Any]]:
        # get joke from the jokes api
        joke = urlopen('https://official-joke-api.appspot.com/random_joke')
        # convert 'string dict' to dict using ast
        joke = literal_eval(joke.read().decode('utf-8'))
        joke = ' ..... '.join([joke['setup'], joke['punchline']])
        dispatcher.utter_message(joke)
        return []
```

### 3. Updating Intents

Amend the **data/nlu.md** file as follows to add new intents for the custom actions:

```markdown
## intent:greet
- hey
- hello
- hi
- good morning
- good evening
- hey there

## intent:goodbye
- bye
- goodbye
- see you around
- see you later

## intent:mood_great
- perfect
- very good
- great
- amazing
- wonderful
- I am feeling very good
- I am great
- I'm good
- I'm fine, thanks
- Fine, thank you
- I am okay
- ok

## intent:mood_unhappy
- sad
- very sad
- unhappy
- bad
- very bad
- awful
- terrible
- not very good
- extremely sad
- so sad
- depressed
- down

## intent:bot_challenge
- are you a bot?
- are you a human?
- am I talking to a bot?
- am I talking to a human?

## intent:math_facts
- random math fact
- Mathematical facts
- Facts from math
- maths facts
- mathematics

## intent:jokes
- tell me a joke
- tell me something funny
- hilarious joke
- jokes

## intent:history
- Historical event
- Today in history
- History
```

### 4. Updating Stories

Create stories for the new intents and custom actions. Modify the **data/stories.md** file as follows:

```markdown
## happy path
* greet
  - utter_greet
* mood_great
  - utter_happy
  - utter_choose_item

## sad path
* greet
  - utter_greet
* mood_unhappy
  - utter_cheer_up
  - utter_choose_item

## say goodbye
* goodbye
  - utter_goodbye

## bot challenge
* bot_challenge
  - utter_iamabot

## tell joke
* jokes
  - get_joke
  - get_joke
  - utter_next

## tell historical facts
* history
  - get_date_fact
  - get_date_fact
  - utter_next

## tell math fact
* math_facts
  - get_math_fact
  - get_math_fact
  - utter_next
  ```

### 5. Updating the Domain

Amend the **domain.yml** to reflect all the changes:

```yaml
intents:
  - greet
  - goodbye
  - affirm
  - deny
  - mood_great
  - mood_unhappy
  - bot_challenge
  - math_facts
  - jokes
  - history

responses:
  utter_greet:
  - text: "Hey! How are you?"

  utter_cheer_up:
  - text: "Oh no! I'm sorry to hear that."

  utter_happy:
  - text: "Awesome!"
  - text: "That's great!"

  utter_goodbye:
  - text: "Bye"

  utter_iamabot:
  - text: "I am a bot, powered by Rasa."

  utter_choose_item:
  - text: "Could I interest you in ..."
    buttons:
    - title: "Random math fact"
      payload: "/math_facts"
    - title: "Hillarious joke"
      payload: "/jokes"
    - title: "Fact about today"
      payload: "/history"

  utter_next:
  - text: 'Enter "jokes", "maths" or "history" for more.'

actions:
- get_math_fact
- get_date_fact
- get_joke

session_config:
  session_expiration_time: 60
  carry_over_slots_to_new_session: true
```

### 6. Running the Action Server

First, un-comment the action endpoint in the **endpoints.yml** file:

```yml
...
action_endpoint:
  url: "http://localhost:5055/webhook"
...
```

Afterwards, open a terminal window, activate the virtual environment with rasa installed, and start the action server:

```bash
$ source env/bin/activate
$ rasa run actions
```

![Rasa action server](/assets/images/articles/rasa_actions.png)

### 7. Training the Chatbot

You'll need to train the chatbot with the updated files in order to get an updated model. Head back to the terminal in which you initialised the project, and run:

```bash
$ rasa train
```

### 8. Talking to Your Chatbot

Launch the chatbot in the command-line interface, and say hello...

```bash
$ rasa shell
```

![Rasa Shell](/assets/images/articles/rasa_shell.png)

# Conclusion

There are so many of *Rasa's* features that haven't been touched on in this simple exercise. If you'd like to keep going, the [Building Assistants](https://rasa.com/docs/rasa/user-guide/building-assistants/) tutorial provides a comprehensive guide to building FAQ and contextual chatbots.

Also, it would be a great idea to peruse *Rasa's* well curated documentation; you'll discover more amazing things that it can do.
