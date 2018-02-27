### NMT with Att:
* test file: test.0
* Tfidf pair: test.1
* NMT result: test.pred
* integrated file: [test.comp](test.comp)

### Pseudo pairs
The Pseudo pairs are generated according to the rule:
* < 10 sentences
* rate > 3 => positive, rate < 3 => negative
* <= 15 words
* Only used pos -> neg pairs (Because the TfIdf pairs for pos <-> neg is many-to-many mapping)
* Split by 8:1:1 to train:dev:test



