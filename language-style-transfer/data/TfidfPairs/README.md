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
 * The TF-IDF pairs are _just_ sentences with high cosine similarity of their TF-IDF vectors. For example, it may pair a neg sentence with a _negative_ sentence in the positive review. 
```
Examples
Bad pair:
they were awful . <The neg part of a pos review>
they were awful .

Good pair: 
i do love starbucks and this one is no different !
i love starbucks but this one is not so great .

Ambiguous pair:
i had heard halo was a good place for it .
one star only just because the halo halo is very good .
```
 * The TF-IDF assigns high similarity to a short sentence which overlaps part of a long sentence. So we constrain the ratio of the longer sentences to the shorter not larger than 1.5
 * Due to some inappropriate mapping illustrated in the first point, the NMT trained on TF-IDF is not accurate.

2. Pros
 * TF-IDF creates abundant pseudo pairs to do supervised neural machine translation
 * This can be a baseline for unsupervised methods
 
