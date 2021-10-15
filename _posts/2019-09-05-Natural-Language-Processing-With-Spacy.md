---
tags: nlp spacy
last_modified_at: 2020-05-26T21:18:00+03:00
---
[*spaCy*][1] is a **powerful**, **feature-rich**, open source [Natural Language Processing (NLP)][2] Python package built by [Explosion][3]. Some of *Explosion*'s fascinating tools are demonstrated [here][4].

*spaCy* is excellent for quickly processing large volumes of text data, and picking out useful information. For instance, performing [sentiment analysis][5] on extensive social media records, and extracting the affiliated [named entities][6] (people, places, organisations, etc).

![displacy demo][7]

(*spaCy*'s **Named Entity Visualiser**, [displaCy][8] in action)

## Linguistic Features

Some of *spaCy*'s [main features][9] include:

- **Tokenization:** splitting text into pieces (i.e words, numbers, punctuation marks, etc) termed 'tokens'.

- **Part-of-Speech Tagging:** classifying the tokens according to their *syntactic functions*, as nouns, verbs, conjunctions, determiners, etc.

- **Named Entity Recognition:** getting the people, places, organisations, dates, events, landmark structures, nationalities, languages, etc. in the text. (Please see [Named Entities][10])

- **Sentiment Analysis:** getting the *positivity* or *negativity* score for a phrase, sentence, or entire document.

- **Lemmatization:** getting the *root form* of the tokens, *without inflections* for tense, plural, case, gender,  etc. This allows words like 'was' and 'be' to be interpreted as similar.

- **Dependency Parsing:** getting the *grammatical structure* i.e the relationships between the tokens in terms of 'subject' or 'object' in the given contexts.

- **Sentence Boundary Detection:** getting the sentences in the text (grouping together tokens that make up individual sentences, by identifying where sentences begin and end).

## Getting Started

A straight-forward way to install *spaCy* would be:

```bash
pip install -U spacy
```

More options, such as installing from source, can be found at [*spaCy*'s usage guide][11].

*spaCy* offers [pretrained models][12]:

- **Core models:** ready to use for predicting named entities, part-of-speech tags and syntactic dependencies. Can be fine-tuned to better fit a case.
- **Starter models:** base models with pretrained weights for use in [Transfer learning][13].

## Basic Usage

```python
>>> from spacy.lang.en import English
>>> nlp = English()
>>> doc = nlp("The quick brown fox jumped over the lazy cat.")
>>> type(doc)
#<class 'spacy.tokens.doc.Doc'>
>>> type(doc[0])  # an individual Token
#<class 'spacy.tokens.token.Token'>
>>> type(doc[0:5])  # a Span, a slice from a Doc
#<class 'spacy.tokens.span.Span'>
```

## Using a Pretrained Model

```bash
# To install the small English core model
$ python -m spacy download en_core_web_sm
$ python
```

```python
>>> import spacy
>>> nlp = spacy.load('en_core_web_sm')
>>> doc = nlp("Jack and Jill ran up the hill.")
>>> doc.ents  # predicted entities
(Jack, Jill)
>>> for entity in doc.ents:  
...     print(entity.text, entity.label_)
...
Jack PERSON
Jill PERSON
>>> for token in doc:  # predicted attributes
...     print(token.text, token.lemma_, token.pos_, token.tag_, token.dep_,
...             token.shape_, token.is_alpha, token.is_stop)
...
Jack Jack PROPN NNP nsubj Xxxx True False
and and CCONJ CC cc xxx True True
Jill Jill PROPN NNP conj Xxxx True False
ran run VERB VBD ROOT xxx True False
up up ADP RP prt xx True True
the the DET DT det xxx True True
hill hill NOUN NN pobj xxxx True False
```

## Next Steps

*spaCy* has its very own [Advanced NLP with *spaCy* course][14], which *explains* and *demonstrates* its features far more elaborately. It also includes *coding sections* for an engaging learning experience. It is offered free of charge. I've tried it... and it's awesome. Please consider checking it out.

[1]: https://spacy.io/
[2]: https://en.wikipedia.org/wiki/Natural_language_processing
[3]: https://explosion.ai/
[4]: https://explosion.ai/software#demos
[5]: https://en.wikipedia.org/wiki/Sentiment_analysis
[6]: https://en.wikipedia.org/wiki/Named_entity
[7]: /assets/images/articles/displacy.png
[8]: https://explosion.ai/demos/displacy-ent
[9]: https://spacy.io/usage/spacy-101#features
[10]: https://spacy.io/api/annotation#named-entities
[11]: https://spacy.io/usage
[12]: https://spacy.io/models
[13]: https://spacy.io/models
[14]: https://course.spacy.io
