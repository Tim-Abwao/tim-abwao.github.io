---
layout: post
author: Abwao
---
[spaCy](https://spacy.io/) is a powerful, open source Natural Language Processing (NLP) software package built by [Explosions AI](https://explosion.ai/). It's very handy for processing large volumes of text, and picking out information about the people/places/companies/etc mentioned. It also has wonderful text visualisation tools, demonstrated [here](https://explosion.ai/demos/).

Some of it's [main features](https://spacy.io/usage/spacy-101#features) include:

- **Tokenization:** splitting text into pieces (i.e words, numbers, punctuation marks, etc) termed 'tokens'.

- **Part-of-Speech Tagging:** classifying the tokens according to their *syntactic functions*, as nouns/verbs/conjunctions/determiners/etc.

- **Named Entity Recognition:** getting the names, places, organisations, dates, events, landmark structures, nationalities, languages, etc. in the text. Please see [Named Entities](https://spacy.io/api/annotation#named-entities).

- **Sentiment Analysis:** gives a positivity/negativity score of a phrase/sentence/document.

- **Lemmatization:** getting the root/base form of the tokens, without inflections for tense/plural/case/gender/ etc. This allows words like 'was' and 'be' to be interpreted as similar.

- **Dependency Parsing:** getting the grammatical structure i.e relationships between the tokens in terms of 'subject' or 'object' in the given contexts.

- **Sentence Boundary Detection:** getting the sentences in the text (grouping together tokens that make up individual sentences by identifying where sentences begin and end).

and many more.
## Getting Started
Installation instructions for the various OS platforms can be found at [spaCy's usage guide](https://spacy.io/usage). (**Note:** On *Windows* OS, installing spaCy with pip requires you to have a Microsoft Visual C++ Compiler installed. You can get it [here](https://visualstudio.microsoft.com/visual-cpp-build-tools/), or you can use `conda` instead)

Spacy has its very own [Advanced NLP with spaCy course](https://course.spacy.io) that introduces and explains its various features; and even includes practice sessions to see them in action. It's the best way to learn what spaCy is all about.

If you wish, you can download and try out a [simple NLP app](https://github.com/Tim-Abwao/spaCy-Text-App) I'd made using *spaCy*.


