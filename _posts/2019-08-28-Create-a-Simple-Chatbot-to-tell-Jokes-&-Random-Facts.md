---
layout: post
author: Abwao
last_modified_at: 2020-05-28T13:19:00+03:00
---

[*Rasa*][1] is an [open source][2] Python package that provides easy-to-use tools for building intelligent text and voice based *assistants*(chatbots).

![rasa logo](/assets/images/articles/rasa-logo.svg)

## Getting Started

You can install *Rasa* using `pip`:

```bash
python3 -m venv venv
source venv/bin/activate
pip install rasa
```

If this doesn't work, you might be missing some dependencies (only Python 3.6 and 3.7 are currently supported):

```bash
sudo apt update
sudo apt install python3-dev
```

For *Windows* and *macOS* users, please refer to the [step-by-step installation guide][3].

## Jokes & Random Facts Chatbot

### 1. Create the project directory and install Rasa

```bash
mkdir chatbot
cd chatbot
python3 -m venv venv
source venv/bin/activate
pip install rasa
```

### 2. Initialize the project

```bash
rasa init --no-prompt
```

This creates all the necessary files, and trains a simple chatbot you can interact with right away in your terminal with:

```bash
rasa shell
```

### 3. Update intents

*Intents* are the things you expect users will say. Add the following *intents* to the file **data/nlu.md**:  

```markdown
## intent:math_facts
- random math fact
- Mathematical facts
- Facts from math
- maths facts

## intent:jokes
- tell me a joke
- tell me something funny
- hilarious joke
- funny jokes

## intent:history
- Historical event
- Today in history
- History
```

### 4. Update stories

A *story* is an example of how conversations would flow between a user and the chatbot. First, modify the *happy path* and *sad path* stories in **data/stories.md** as follows:

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
```

Afterwards, add these stories for the new intents:

```markdown
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

### 5. Add Custom Actions

*Actions* are things the chatbot can perform in response to user input. We'll need to define [custom actions][4] to fetch the fact & joke content. Custom actions are created as Python classes.

Add the following to the **actions.py** file:

```python
from typing import Any, Text, Dict, List
from rasa_sdk import Action, Tracker
from rasa_sdk.executor import CollectingDispatcher
import requests
from datetime import date


class ActionGetMathFact(Action):

    def name(self) -> Text:
        return "get_math_fact"

    def run(self, dispatcher: CollectingDispatcher, tracker: Tracker,
            domain: Dict[Text, Any]) -> List[Dict[Text, Any]]:
        """Get a random math fact and utter it as a response."""
        fact = requests.get('http://numbersapi.com/random/trivia')
        dispatcher.utter_message(fact.text)
        return []


class ActionGetDateFact(Action):

    def name(self) -> Text:
        return "get_date_fact"

    def run(self, dispatcher: CollectingDispatcher, tracker: Tracker,
            domain: Dict[Text, Any]) -> List[Dict[Text, Any]]:
        """Get a random fact about current day and utter it as a response."""
        today = date.strftime(date.today(), '%m/%d')
        day_fact = requests.get(f'http://numbersapi.com/{today}/date')
        dispatcher.utter_message(day_fact.text)
        return []


class ActionGetJoke(Action):

    def name(self) -> Text:
        return "get_joke"

    def run(self, dispatcher: CollectingDispatcher, tracker: Tracker,
            domain: Dict[Text, Any]) -> List[Dict[Text, Any]]:
        """Get a joke and utter it as a respose."""
        joke = (requests.get('https://official-joke-api.appspot.com/random_joke')
                        .json())
        joke_text = f"{joke['setup']}...  {joke['punchline']}."
        dispatcher.utter_message(joke_text)
        return []
```

### 6. Update the domain

The domain defines the chatbot's world - all that it knows and can do. Amend the **domain.yml** file to reflect the above additions:

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
  - text: "Here is something to cheer you up:"
    image: "https://i.imgur.com/nGF1K8f.jpg"

  utter_did_that_help:
  - text: "Did that help you?"

  utter_happy:
  - text: "Great, carry on!"

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

### 7. Train the chatbot

The *assistant* has to be re-trained with the updated files, in order to obtain a model that includes the added features.

```bash
rasa train
```

### 8. Run the action server

First, you'll need to un-comment the *action_endpoint* in the **endpoints.yml** file. Delete the leading `#` in the two lines to get:

```yml
...
action_endpoint:
  url: "http://localhost:5055/webhook"
...
```

Afterwards, open a new terminal tab or window at the project folder, activate the virtual environment, and start the action server:

```bash
source venv/bin/activate
rasa run actions
```

![Rasa action server](/assets/images/articles/rasa-actions.gif)

### 9. Try out your assistant

Launch the chatbot, and say hey...

```bash
rasa shell
```

![Rasa Shell](/assets/images/articles/rasa-shell.gif)

## Next Steps

At its current state, the chatbot will probably give some surprising responses. It needs further training. And there are so many of *Rasa's* features that haven't been touched on in this simple exercise, which could greatly improve it.

If you'd like to keep going, the [Building Assistants][5] tutorial provides a comprehensive guide to building FAQ and contextual-conversation chatbots. Also, it would be a great idea to peruse *Rasa's* well curated documentation; you'll discover more amazing things it can do.

[1]: https://rasa.com/
[2]: https://opensource.com/resources/what-open-source
[3]: https://rasa.com/docs/rasa/user-guide/installation/#step-by-step-installation-guide
[4]: https://rasa.com/docs/rasa/core/actions/#custom-actions
[5]: https://rasa.com/docs/rasa/user-guide/building-assistants/
