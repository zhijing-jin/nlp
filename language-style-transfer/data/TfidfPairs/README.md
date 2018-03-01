### NMT with Att:
* prediction (long sentences): [test.comp](long_sent/test.comp)
* prediction (15-word sentences): [test.comp](15words_sent/test.comp)

### Pseudo pairs
The Pseudo pairs are generated according to the rule:
* < 10 sentences
* rate > 3 => positive, rate < 3 => negative
* Only used pos -> neg mapping
* Then they are split by 8:1:1 to train:dev:test

### Pros and Cons for TF-IDF Pseudo Pairs
#### Cons:
 * For certain datasets or small datasets, it's hard to match corresponding opposite sentences in the training set.
 * For long sentences, there is no off-hand exact match.
 * The TF-IDF pairs are _just_ sentences with high cosine similarity of their TF-IDF vectors. For example, it may pair a neg sentence with a _negative_ sentence in the positive review. 
```
Examples

Good pair: 
i do love starbucks and this one is no different !
i love starbucks but this one is not so great .

Bad pair:
they were awful . <The neg part of a pos review>
they were awful .

Ambiguous pair:
i had heard halo was a good place for it .
one star only just because the halo halo is very good .
```
 * The TF-IDF assigns high similarity to a short sentence which overlaps part of a long sentence. So we constrain the ratio of the longer sentences to the shorter not larger than 1.5
 * Due to some inappropriate mapping illustrated in the first point, the NMT trained on TF-IDF is not accurate.

#### Pros
 * TF-IDF creates abundant pseudo pairs to do supervised neural machine translation
 * TF-IDF captures lots of sentences with same nouns (same content), but with different sentiment because they are in positive and negative sets.
 * This can be a baseline for unsupervised methods

 ```
this is my favorite mexican food restaurant in the valley .
so , this mexican restaurant is just like any other mexican restaurant in the valley .
this is not my favorite mexican restaurant .
 ```

### Analysis of NMT with Pseudo Pairs


#### BAD PAIRS

    cool atmosphere inside .
    cool atmosphere .
    cool atmosphere .

    nice modern art .
    it 's modern !
    nice art art .

    service is great too
    service is great .
    service is great .

    best prime rib in the valley !
    prime rib was the best there .
    prime rib was the best there .

    they 're very accommodating and helpful .
    very helpful , very nice and accommodating !
    the staff was very helpful and accommodating .







#### GOOD PAIRS

    best dental stuff of my life .
    this was the worst dental experience of my life .
    worst dental experience of my life .

    reminds me of restaurants in italy .
    it reminds me of frozen food ...
    it reminds me of frozen food ...

    i would go here again for the price .
    i would n't go here again .
    i would n't go here again .



#### AMBIGUOUS

    one of my favorite places in downtown champaign .
    i miss the old downtown champaign location .
    this used to be one of my favorite places .
