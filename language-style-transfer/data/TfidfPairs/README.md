### NMT with Att:
* prediction (long sentences): [test.comp](long_sent/test.comp)
* prediction (15-word sentences): [test.comp](15words_sent/test.comp)

### Pseudo pairs
The Pseudo pairs (15words.0 and 15words.1) are generated according to the rule:
* < 10 sentences
* rate > 3 => positive, rate < 3 => negative
* Only used pos -> neg mapping
* Then they are split by 8:1:1 to train:dev:test

### Pros and Cons for TF-IDF Pseudo Pairs
1. Cons:
 1. * The TF-IDF pairs are sentences with high cosine similarity of their TF-IDF vectors. For example, it may pair a neg sentence with a _negative_ sentence in the positive review. 
Eg. 
Bad pair:
they were awful . <The neg part of a pos review>
they were awful .

Good pair: 
i do love starbucks and this one is no different !
i love starbucks but this one is not so great .

Ambiguous pair:
i had heard halo was a good place for it .
one star only just because the halo halo is very good .

* 
