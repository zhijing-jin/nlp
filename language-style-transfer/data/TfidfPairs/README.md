### NMT with Att:
* prediction (long sentences): [test.comp](long_sent/test.comp)
* prediction (15-word sentences): [test.comp](15words_sent/test.comp)

### Pseudo pairs
The Pseudo pairs (15words.0 and 15words.1) are generated according to the rule:
* < 10 sentences
* rate > 3 => positive, rate < 3 => negative
* Only used pos -> neg mapping
* Then they are split by 8:1:1 to train:dev:test



