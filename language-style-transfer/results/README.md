
|  |  |  |  |
|---|---| ---|---|---|
| aa | 01121705 | style_transfer | paper setting | python style_transfer.py --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/01091053 --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --model ../data/runtime/models/01091053.model |
| ab | 01131502 | classifier | paper setting | python classifier.py --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --model ../data/runtime/models/clf_real.model |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
