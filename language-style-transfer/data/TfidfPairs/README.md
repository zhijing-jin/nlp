1. Trained by NMT with Att:
* test file: test.0
* Tfidf pair: test.1
* NMT result: test.pred
* integrated file: [test.comp](test.comp)

2. The Pseudo pairs (15words.0 and 15words.1) are generated according to the rule:
* < 10 sentences
* rate > 3 => positive, rate < 3 => negative
* <= 15 words
* Only used pos -> neg to generate 15words.1 -> 15words.0 (Because the TfIdf pairs for pos <-> neg is many-to-many mapping)
* Then they are split by 8:1:1 to train:dev:test



