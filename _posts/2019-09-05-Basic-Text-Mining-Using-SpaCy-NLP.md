---
layout: post
author: Abwao
---
[spaCy](https://spacy.io/) is a **powerful**, **convenient**, open source **Natural Language Processing (NLP)** Python package built by [Explosions AI](https://explosion.ai/). It is excellent for quickly processing large volumes of text and picking out information about the entities (people/places/organisations/etc) present. It also has wonderful text visualisation tools, demonstrated [here](https://explosion.ai/demos/).

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
Installation instructions can be found at [spaCy's usage guide](https://spacy.io/usage). The customisation-form there helps configure your install for a particular Operating System, Python Package Manager, Python version, Language and a few extra options.

Spacy has its very own [Advanced NLP with spaCy course](https://course.spacy.io) which *exlains* and *demonstrates* its more advanced features. The included *practice sessions* let you see it in action. This is probably the best way to learn what spaCy is all about.

## Next Steps
If you're interested in trying spaCy out for yourself, you can download and test  [this simple NLP app](https://github.com/Tim-Abwao/text-mining-spacy). It's intended to extract text from documents in a multitude of formats, and derive named-entity information. Feel free to make adjustments and improvements.


