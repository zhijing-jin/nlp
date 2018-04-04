## Overall Results
### 1. Newest Updates
#### (1.1) Style Transfer (<15 words)
- 20 epoch -> 78.57%

#### (1.2) Noise Model
- normal style_transfer (20 epoch)      -> 78.57%
- noise model with permute+dropout  -> 83.69%   (rho=0.3 & gamma=0.5)

#### (1.3) Antonym Method
- normal style_transfer (20 epoch)      -> 78.57%
- substitute all adj. with antonyms      -> 42.11%
- substitute all adj. + BOW top1000 words with antonyms -> 48.81%
- substitute all BOW top1000 words with antonyms           -> 45.70%
- substitute all BOW top1000 words with antonyms, and only keep changed sentences -> 75.16%

#### (1.4) Pseudo Pairs with NMT (attention)
- pseudo sentence pairs by cosine similarity of TF-IDF: 
https://github.com/zhijing-jin/nlp/tree/master/language-style-transfer/data/TfidfPairs
- sample results for 15-word sentences (Original | Pseudo Pair | NMT) -> 可以scroll down看一下后面的长句子:
https://github.com/zhijing-jin/nlp/blob/master/language-style-transfer/data/TfidfPairs/long_sent/test.comp
- sample results for 15-word sentences (Original | Pseudo Pair | StyleTransfer):
https://raw.githubusercontent.com/zhijing-jin/nlp/master/language-style-transfer/results/01141156.compare.1.tsf
- sample results for long sentences (Original | Pseudo Pair | NMT) -> 可以scroll down看一下后面的长句子:
https://github.com/zhijing-jin/nlp/blob/master/language-style-transfer/data/TfidfPairs/long_sent/test.comp


### 2. Google Sheet of Progress:
https://docs.google.com/spreadsheets/d/10oth0gMC0Ywy2CWVxSzvcnF4GVkKzh3SpPO-HAbIlQg/edit#gid=0

### 3. Github repository:
https://github.com/zhijing-jin/nlp/tree/master/language-style-transfer


#### Appendix: Past Tries



| model | time | type | setting | command |
|---|---| ---|---|---|
| aa | 01121705 | style_transfer | paper setting | python style_transfer.py --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/01091053 --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --model ../data/runtime/models/01091053.model |
| ab | 01131502 | classifier | paper setting | python classifier.py --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --model ../data/runtime/models/clf_real.model |
| ac | 01141149 | style_transfer | with shuffled noise | python style_transfer.py --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/ac/01141149 --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --model ../data/runtime/ac/01141149.model |
| ad | 01141156 | style_transfer | with shuffled + dropped noise | python style_transfer.py  --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/ad/01141156 --model ../data/runtime/ad/01141156.model |
| ae | 01152211 | style_transfer | with shuffled noise & rho=0.5 | python style_transfer.py  --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/ae/01152211 --model ../data/runtime/ae/01152211.model --rho 0.5 --max_epochs 40 |
| af | 01152216 | style_transfer | with shuffled noise & rho=0.3 | CUDA_VISIBLE_DEVICES=0 python style_transfer.py  --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/af/01152216 --model ../data/runtime/af/01152216.model --rho 0.3 --max_epochs 40 --gamma_init 0.001 --load_model True |
| ag | 01162311 | style_transfer | with shuffled noise & rho=0.3 & gamma=0.5 -> g_loss=15, acc=79 | python style_transfer.py  --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/ag/01162311 --model ../data/runtime/ag/01162311.model --rho 0.3 --gamma_init 0.5 --gamma_decay 0.2 --max_epochs 400 |
| ah | 01162320 | style_transfer | with shuffled noise & rho=0.3 & gamma=0.8 | python style_transfer.py  --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --train ../data/sentiment.train --dev ../data/sentiment.dev --test ../data/sentiment.test --output ../data/runtime/ah/01162320 --model ../data/runtime/ah/01162320.model --rho 0.3 --gamma_init 0.8 --gamma_decay 0.3 --max_epochs 400 |
| aj | 03301140 | nmt | single encoder for 1->0 and 0->1, batch is 1<->0, when passing in y0 you should not use an all-zero vector | CUDA_VISIBLE_DEVICES=0 python python style_transfer_aj.py --train ../code/baselines/mt/nmt-tf/nmt/testdata/train --dev ../code/baselines/mt/nmt-tf/nmt/testdata/tst2013 --test ../code/baselines/mt/nmt-tf/nmt/testdata/tst2012 --output ../data/runtime/aj/03301705 --vocab ../data/runtime/vocab_ted.0 --vocab1 ../data/runtime/vocab_ted.1 --embedding ../data/glove.6B.100d.pruned.txt --embedding1 ../code/baselines/mt/nmt-tf/nmt/testdata/vocab.1 --model ../data/runtime/aj/03301705.model |
| ak | 02120938 | att | learning_rate 0.00001 | CUDA_VISIBLE_DEVICES=1 python att.py --train ../data/runtime/ti2/pos2neg/train --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --dev ../data/runtime/ti2/pos2neg/dev --test ../data/runtime/ti2/pos2neg/test --output ../data/runtime/ak/02120938 --model ../data/runtime/at/02090154checkp.ep49.pth.tar --max_epochs 500 --batch_size 1024 --learning_rate 0.00001 |
| al | 04031150 | nmt | success | CUDA_VISIBLE_DEVICES=0 python python style_transfer_al.py --train ../../data/runtime/ed/train --dev ../../data/runtime/ed/dev --test ../../data/runtime/ed/test --output ../../data/runtime/al/04031150 --vocab ../../data/runtime/ed/vocab100.0 --vocab1 ../../data/runtime/ed/vocab100.1 --embedding ../../data/runtime/eg/glove.6B.300d.txt --embedding1 ../../data/runtime/eg/glove.de.300d.txt --model ../../data/runtime/al/04031150.model --dim_emb 300 --batch_size 64 --max_train_size 90000 --learning_rate 0.01 --max_epochs 20 |
| am | 04031934 | visual | original style_tr, for visualization | CUDA_VISIBLE_DEVICES=1 python python style_transfer.py --train ../../data/runtime/yf/sentiment.train.uniq --dev ../../data/runtime/yf/sentiment.dev --test ../../data/runtime/yf/sentiment.test --output ../../data/runtime/am/04031934 --vocab ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/am/04031934.model --dim_emb 100  |
| at | 02120232 | att | no teacher forcing, learning_rate 0.000001 | CUDA_VISIBLE_DEVICES=2 python att.py --train ../data/runtime/ti2/pos2neg/train --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --dev ../data/runtime/ti2/pos2neg/dev --test ../data/runtime/ti2/pos2neg/test --output ../data/runtime/at/02120232 --model ../data/runtime/at/02090154checkp.ep49.pth.tar --max_epochs 500 --batch_size 1024 --learning_rate 0.000001 |
|  | 02242102 | att | 15 words, tfidf pairs hollow, filtered 1.5 ratio |  |
|  | 02261711 | att | long sent, filtered 1.5 ratio |  |

| ao |  | mt for tfidf pairs |  | CUDA_VISIBLE_DEVICES=0 python python style_transfer_al.py --train ../../code/baselines/mt/OpenNMT-py/data/train --dev ../../code/baselines/mt/OpenNMT-py/data/dev --test ../../code/baselines/mt/OpenNMT-py/data/test --output ../../data/runtime/ao/04040722 --vocab ../../data/runtime/am/vocab --vocab1 ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --embedding1 ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/ao/04040722.model --dim_emb 100 --batch_size 64 --learning_rate 0.01 --max_epochs 20 |
| ap |  | changing y to emb |  | CUDA_VISIBLE_DEVICES=2 python python style_transfer_y.py --train ../../data/runtime/yf/sentiment.train.uniq --dev ../../data/runtime/yf/sentiment.dev --test ../../data/runtime/yf/sentiment.test --output ../../data/runtime/ap/04040829 --vocab ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/ap/04040829.model --dim_emb 100 |
|  |  |  |  |  |
