This repository stores yelp reviews that has been modified by changing all adjectives to their antonyms.

The antonyms are from nltk.wordnet and a customized list for common antonym pairs.

:)

==LIMITATION ANALYSIS==
- Not every word has an antonym available in wordnet, for example "superb" doesn't.
- Hard for nltk library to correctly mark all POS, eg. it distinguishes "disgusting" as a verb.
- There are neutral or informative words like "other", "eastern", "first->last" that shouldn't be changed.
- Changing the word to its antonym somtimes does not result in natural sentences, eg. "It is obvious that...".
- Changing an even number of antonyms may offset the change or distort the sentence a little
- Some verbs like "like", "disgust" as well as adverbs like "greatly", "agreeably" also implies sentiment
