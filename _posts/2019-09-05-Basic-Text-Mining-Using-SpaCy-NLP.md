---
layout: post
author: Abwao
last_modified_at: 2020-04-25T16:58:09+03:00
---
[spaCy](https://spacy.io/) is a **powerful**, **convenient**, open source **Natural Language Processing (NLP)** Python package built by [Explosions AI](https://explosion.ai/).

It is excellent for quickly processing large volumes of text and picking out information about the entities (people/places/organisations/etc) present. It also has wonderful text visualisation tools, demonstrated [here](https://explosion.ai/demos/).

![displacy demo](/assets/images/articles/displacy.png)<br>
<sub> *spaCy's Named Entity Visualiser <a href="https://explosion.ai/demos/displacy-ent">displaCy</a> in action*</sub>

## Linguistic Features

Some of spaCy's [main features](https://spacy.io/usage/spacy-101#features) include:

- **Tokenization:** splitting text into pieces (i.e words, numbers, punctuation marks, etc) termed 'tokens'.

- **Part-of-Speech Tagging:** classifying the tokens according to their *syntactic functions*, as nouns/verbs/conjunctions/determiners/etc.

- **Named Entity Recognition:** getting the names, places, organisations, dates, events, landmark structures, nationalities, languages, etc. in the text. Please see [Named Entities](https://spacy.io/api/annotation#named-entities).

- **Sentiment Analysis:** gives the positivity/negativity score for a phrase/sentence/document.

- **Lemmatization:** getting the root/base form of the tokens, without inflections for tense/plural/case/gender/ etc. This allows words like 'was' and 'be' to be interpreted as similar.

- **Dependency Parsing:** getting the grammatical structure i.e relationships between the tokens in terms of 'subject' or 'object' in the given contexts.

- **Sentence Boundary Detection:** getting the sentences in the text (grouping together tokens that make up individual sentences by identifying where sentences begin and end).

## Getting Started

Detailed [installation instructions](https://spacy.io/usage) can be found at spaCy's usage guide. This is the recommended way to get it.

A straight-forward way would be to intall from PyPi with:

```bash
$pip install -U spacy
```

Next, add a [model](https://spacy.io/models) to use:

```bash
# to get the small core model in English
python -m spacy download en_core_web_sm
```

## Basic Usage

```python
import spacy
nlp = spacy.load("en_core_web_sm")
doc = nlp("This is a sentence.")
```

Spacy has its very own [Advanced NLP with spaCy course](https://course.spacy.io) which *exlains* and *demonstrates* its features. The included *practice sessions* let you see it in action. This is probably the best way to learn what spaCy is all about.

## Next Steps

If you're interested in trying spaCy out for yourself, you can download and test  [this simple NLP app](https://github.com/Tim-Abwao/text-mining-spacy). It's intended to extract and process text from documents in all sorts of formats, then output the named-entities present. Feel free to make adjustments and improvements.
