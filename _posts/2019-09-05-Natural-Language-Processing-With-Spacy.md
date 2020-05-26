---
layout: post
author: Abwao
last_modified_at: 2020-05-26T21:18:00+03:00
---
[spaCy](https://spacy.io/) is a **powerful**, **feature-rich**, open source **Natural Language Processing (NLP)** Python package built by [Explosion AI](https://explosion.ai/).

It is excellent for quickly processing large volumes of text, and picking out useful information; for instance the entities (people/places/organisations/etc) present. It also has wonderful text visualisation tools, demonstrated [here](https://explosion.ai/demos/).

![displacy demo](/assets/images/articles/displacy.png)<br>
<sub> *spaCy's Named Entity Visualiser <a href="https://explosion.ai/demos/displacy-ent">displaCy</a> in action*</sub>

## Linguistic Features

Some of spaCy's [main features](https://spacy.io/usage/spacy-101#features) include:

- **Tokenization:** splitting text into pieces (i.e words, numbers, punctuation marks, etc) termed 'tokens'.

- **Part-of-Speech Tagging:** classifying the tokens according to their *syntactic functions*, as nouns/verbs/conjunctions/determiners/etc.

- **Named Entity Recognition:** getting the names, places, organisations, dates, events, landmark structures, nationalities, languages, etc. in the text. (Please see [Named Entities](https://spacy.io/api/annotation#named-entities))

- **Sentiment Analysis:** gives the positivity/negativity score for a phrase/sentence/document.

- **Lemmatization:** getting the root/base form of the tokens, without inflections for tense/plural/case/gender/ etc. This allows words like 'was' and 'be' to be interpreted as similar.

- **Dependency Parsing:** getting the grammatical structure i.e relationships between the tokens in terms of 'subject' or 'object' in the given contexts.

- **Sentence Boundary Detection:** getting the sentences in the text (grouping together tokens that make up individual sentences by identifying where sentences begin and end).

## Getting Started

A straight-forward way to intall spaCy would be:

```bash
$ pip install -U spacy
```

More options, such as installing from source, can be found at [spaCy's usage guide](https://spacy.io/usage).

spaCy offers [pretrained model](https://spacy.io/models):

- **Core models:** ready to use for predicting named entities, part-of-speech tags and syntactic dependencies. Can be fine-tuned to better fit a case.
- **Starter models:** base models with pretrained weights for use in Transfer learning.

## Basic Usage

```python
>>> from spacy.lang.en import English
>>> nlp = English()
>>> doc = nlp("The quick brown fox jumped over the lazy cat")
>>> type(doc)
#<class 'spacy.tokens.doc.Doc'>
>>> type(doc[0])  # an individual Token
#<class 'spacy.tokens.token.Token'>
>>> type(doc[0:5])  # a Span, a slice from a Doc
#<class 'spacy.tokens.span.Span'>
```

### Using a pretrained model

```bash
# To install the small English core model
$ python -m spacy download en_core_web_sm
$ python
```

```python
>>> import spacy
>>> nlp = spacy.load('en_core_web_sm')
>>> doc = nlp("Jack and Jill ran up the hill.")
>>> doc.ents  # named entity recognition
(Jack, Jill)
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
>>> for entity in doc.ents:  
...     print(entity.text, entity.label_)
...
Jack PERSON
Jill PERSON

```

## Next Steps

Please consider taking the  [Advanced NLP with spaCy course](https://course.spacy.io), which *exlains* and *demonstrates* its features far more elaborately. It includes *coding sections* for an engaging learning experience. I've tried it... and its awesome.
