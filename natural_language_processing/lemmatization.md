---
description: Lemmatization
---

# Lemmatization

With `TextBlob`

```python
from textblob import TextBlob, Word

w = Word('adoration')
w.lemmatize()
```

With `spaCy`

```bash
python -m spacy download en_core_web_sm
```

(note: the above will not work with poetry, where we'll have to add the package `en_core_web_sm` explicitly to poetry by specifying its url)

```python
import spacy

nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner']) # just keep tagger for lemmatization
" ".join([token.lemma_ for token in nlp('adoration adore adoring')])
```

## Note

Source: https://stackoverflow.com/questions/59636002/spacy-lemmatization-of-a-single-word/59636107#59636107

    Lemmatization crucially depends on the part of speech of the token. Only tokens with the same part of speech are mapped to the same lemma.

    In the sentence "This is confusing", confusing is analyzed as an adjective, and therefore it is lemmatized to confusing. In the sentence "I was confusing you with someone else", by contrast, confusing is analyzed as a verb, and is lemmatized to confuse.

    If you want tokens with different parts of speech to be mapped to the same lemma, you can use a stemming algorithm such as Porter Stemming (Java), which you can simply call on each token.

```python
import spacy
from spacy.lemmatizer import Lemmatizer
from spacy.lookups import Lookups
lookups = Lookups()
lemmatizer = Lemmatizer(lookups)

word = "ducks"
#load spacy core database
nlp = spacy.load('en_core_web_sm')
#run NLP on input/doc
doc = nlp(word)
#Print formatted token attributes
print("Token Attributes: \n", "token.text, token.pos_, token.tag_, token.dep_, token.lemma_")
for token in doc:
    # Print the text and the predicted part-of-speech tag
    print("{:<12}{:<12}{:<12}{:<12}{:<12}".format(token.text, token.pos_, token.tag_, token.dep_, token.lemma_))
```
