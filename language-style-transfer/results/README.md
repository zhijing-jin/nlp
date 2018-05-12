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
| am | 04031934 | visual | am/04031934.sent_emb:<br>original style_tr, original data, for visualization<br><br><br>am/04061609.sent_emb 1,293,541\*2 sents:<br>yj/train <=15words, dev_loss 16.26, 30 epochs<br><br><br>am/04141040<br>yj/small/train<br>final dataset but 0.3mill sentences  | CUDA_VISIBLE_DEVICES=1 python python style_transfer.py --train ../../data/runtime/yf/sentiment.train.uniq --dev ../../data/runtime/yf/sentiment.dev --test ../../data/runtime/yf/sentiment.test --output ../../data/runtime/am/04031934 --vocab ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/am/04031934.model --dim_emb 100;;;;;;;;;;; CUDA_VISIBLE_DEVICES=1 python python style_transfer.py --train ../../data/runtime/yj/train --dev ../../data/runtime/yj/dev --test ../../data/runtime/yj/test --output ../../data/runtime/am/04061609 --vocab ../../data/runtime/am/vocab04061609 --embedding ../../data/glove.6B.100d.txt --model ../../data/runtime/am/04061609.model --dim_emb 100<br><br>CUDA_VISIBLE_DEVICES=0 python2 python2 style_transfer_az.py --train ../../data/runtime/yj/refined/train --dev ../../data/runtime/yj/refined/dev --test ../../data/runtime/yj/refined/test --vocab ../../data/runtime/az/04101533.vocab --embedding ../../data/glove.6B.100d.txt --output ../../data/runtime/am/04111130 --model ../../data/runtime/am/04111130.model --dim_emb 100 --batch_size 32 --learning_rate 0.0001 --max_epochs 30 --vocab_min_occur 300<br><br>(xiao) zhijing@rosetta11:/scratch/zhijing/language_style_transfer/code/01_ori$ CUDA_VISIBLE_DEVICES=2 python2 python2 style_transfer.py --train ../../data/runtime/yj/small/train --dev ../../data/runtime/yj/small/dev --test ../../data/runtime/yj/small/test --embedding ../../data/glove.6B.100d.txt --vocab ../../data/runtime/am/04141040.vocab --output ../../data/runtime/am/04141040 --model ../../data/runtime/am/04141040.model --dim_emb 100 --batch_size 64 --learning_rate 0.0001 --max_epochs 20 --vocab_min_occur 10 --rho 1 |
|  |  |  | To generate sent_emb (1) | (3_vi) CUDA_VISIBLE_DEVICES=1 python python style_transfer.py --train ../../data/runtime/yf/sentiment.train.uniq --dev ../../data/runtime/yf/sentiment.dev --test ../../data/runtime/yf/sentiment.test --output ../../data/runtime/am/04040712 --vocab ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/am/04040712.model --dim_emb 100 --load_model True |
|  |  |  | To generate sent_emb (2) | python projector.py --output ../../data/runtime/am/04040712 ; tensorboard --logdir=. |
| ao |  | mt for tfidf pairs | look nice | CUDA_VISIBLE_DEVICES=0 python python style_transfer_al.py --train ../../code/baselines/mt/OpenNMT-py/data/train --dev ../../code/baselines/mt/OpenNMT-py/data/dev --test ../../code/baselines/mt/OpenNMT-py/data/test --output ../../data/runtime/ao/04040722 --vocab ../../data/runtime/am/vocab --vocab1 ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --embedding1 ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/ao/04040722.model --dim_emb 100 --batch_size 64 --learning_rate 0.01 --max_epochs 20 |
| ap | 04040829 | changing y to emb, looks better |  | CUDA_VISIBLE_DEVICES=2 python python style_transfer_y.py --train ../../data/runtime/yf/sentiment.train.uniq --dev ../../data/runtime/yf/sentiment.dev --test ../../data/runtime/yf/sentiment.test --output ../../data/runtime/ap/04040829 --vocab ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/ap/04040829.model --dim_emb 100 |
| aq | 04041956 | changing y to emb, y1+y0=0 |  | CUDA_VISIBLE_DEVICES=0 python python style_transfer_y.py --train ../../data/runtime/yf/sentiment.train.uniq --dev ../../data/runtime/yf/sentiment.dev --test ../../data/runtime/yf/sentiment.test --output ../../data/runtime/aq/04041956 --vocab ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/aq/04041956.model --dim_emb 100 |
| ar | 04052021 | nmt | with y_emb | CUDA_VISIBLE_DEVICES=0 python python style_transfer_ar.py --train ../../data/runtime/ed/train --dev ../../data/runtime/ed/dev --test ../../data/runtime/ed/test --output ../../data/runtime/ar/04052021 --vocab ../../data/runtime/ed/vocab100.0 --vocab1 ../../data/runtime/ed/vocab100.1 --embedding ../../data/runtime/eg/glove.6B.300d.txt --embedding1 ../../data/runtime/eg/glove.de.300d.txt --model ../../data/runtime/ar/04052021.model --dim_emb 300 --batch_size 64 --max_train_size 90000 --learning_rate 0.01 --max_epochs 20 |
| as | 04052104 | nmt for tfidf pairs | with y_emb | CUDA_VISIBLE_DEVICES=0 python python style_transfer_ar.py --train ../../code/baselines/mt/OpenNMT-py/data/train --dev ../../code/baselines/mt/OpenNMT-py/data/dev --test ../../code/baselines/mt/OpenNMT-py/data/test --output ../../data/runtime/as/04052104 --vocab ../../data/runtime/am/vocab --vocab1 ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --embedding1 ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/as/04052104.model --dim_emb 100 --batch_size 64 --learning_rate 0.01 --max_epochs 20 |
| au | 04060827 | original style_transfer | 10-sent reviews: 2mill train, 0.6 mill dev, 0.3 mill test | CUDA_VISIBLE_DEVICES=1 python python style_transfer.py --train ../../data/runtime/yj/train --dev ../../data/runtime/yj/dev --test ../../data/runtime/yj/test --output ../../data/runtime/au/04060827 --vocab ../../data/runtime/au/vocab --embedding ../../data/glove.6B.100d.txt --model ../../data/runtime/au/04060827.model --dim_emb 100 |
|  |  |  |  |  |
| aw | 04060938 |  | nmt, y_emb, bidirectional | CUDA_VISIBLE_DEVICES=0 python python style_transfer_aw.py --train ../../code/baselines/mt/OpenNMT-py/data/train --dev ../../code/baselines/mt/OpenNMT-py/data/dev --test ../../code/baselines/mt/OpenNMT-py/data/test --vocab ../../data/runtime/am/vocab --vocab1 ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --embedding1 ../../data/glove.6B.100d.pruned.txt --output ../../data/runtime/aw/04060938 --model ../../data/runtime/aw/04060938.model --dim_emb 100 --batch_size 64 --learning_rate 0.01 --max_epochs 20 |
|  |  |  |  |  |
| az | 04101533 | style_trans with pseudo pairs |  | CUDA_VISIBLE_DEVICES=0 python2 python2 style_transfer_az.py --train ../../data/runtime/yj/refined/train --dev ../../data/runtime/yj/refined/dev --test ../../data/runtime/yj/refined/test --vocab ../../data/runtime/az/04101533.vocab --embedding ../../data/glove.6B.100d.txt --output ../../data/runtime/az/04101533 --model ../../data/runtime/az/04101533.model --dim_emb 100 --batch_size 32 --learning_rate 0.0001 --max_epochs 20 --vocab_min_occur 300 |
|  |  |  |  |  |
| bc |  | style_transfer with better hyperparameters |  |  |
| bd |  | another style_trans with pseudo pairs |  |  |
| be | 05042050 | nmt with tf-idf pairs |  | CUDA_VISIBLE_DEVICES=0 python train.py -save_model runtime_models/05042050 -batch_size 64 -layers 2 \-rnn_size 500 -word_vec_size 100 -pre_word_vecs_enc "./data/05042050.embeddings.enc.pt" -pre_word_vecs_dec "./data/05042050.embeddings.dec.pt" -data ./data/reparti.cut50  -gpuid 0 |
| bf |  | DeleteAndRetrieval |  | I cloned Li Juncen's model, amended the python2.decode, and added more "echo" statements |
| bg |  | DeleteAndRetrieval |  | Trained on 100k data |
|  |  |  |  |  |
| bj |  | DeleteAndRetrieval, 100k, 30 epoch |  |  |
| bi |  | results for DeleteAndRetreival |  | the log.output is in ../bf<br>The ep31 is the best output (MinLen=1)<br>The DeleteAndRetrieval_ep01 and ep30 has some "","None" in them (MinLen=9) |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
| at | 02120232 | att | no teacher forcing, learning_rate 0.000001 | CUDA_VISIBLE_DEVICES=2 python att.py --train ../data/runtime/ti2/pos2neg/train --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --dev ../data/runtime/ti2/pos2neg/dev --test ../data/runtime/ti2/pos2neg/test --output ../data/runtime/at/02120232 --model ../data/runtime/at/02090154checkp.ep49.pth.tar --max_epochs 500 --batch_size 1024 --learning_rate 0.000001 |
|  | 02242102 | att | 15 words, tfidf pairs hollow, filtered 1.5 ratio |  |
|  | 02261711 | att | long sent, filtered 1.5 ratio |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
| ti |  | tfidf pairs for yk | / |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
| yf |  | 2017nips | original dataset | 159507 sentiment.train.uniq.0<br>  224451 sentiment.train.uniq.1<br> 25602 sentiment.dev.0<br>   38292 sentiment.dev.1<br>   51206 sentiment.test.0<br>   76584 sentiment.test.1   |
|  |  |  |  |  |
| yh |  | 2018yelp (restaurant) |  | 1. Number of Businesses<br>	number of all Yelp businesses：  		174,567		business.json<br>	number of restaurant businesses：      	72,065		review.resta_id<br>2. Reviews<br>	Total reviews：	    					5,261,669	review.json <br>	Restaurant reviews： 					3,635,685	review.rate_n_sent <br>		Sentence-by-sentence restaurant reviews:	36,628,355 review.nice.multilingual<br>	Sentence-by-sentence restaurant reviews (9268 English vocab):	36,621,804 review.nice |
| yi |  | 2018yelp (restaurant), split |  |    2687937 yi/sent_to10.0<br>   8689184 yi/sent_to10.1<br>    893517 yi/sent_to5.0<br>   3417738 yi/sent_to5.1<br> |
| yj |  | senti_clf dataset<br><br>/refined:<br>added original pos2neg | 2018yelp, 10sent reviews, same pos & neg number, <= 15-word sents | 1293541句 ../yj/train.0; 71863句 ../yj/test.1 |
| yk |  | overall dataset | 2018yelp, 10sent reviews, excluded testsets, long sents | 134359 yk/longsente.dev.0<br>   434386 yk/longsente.dev.1<br>   134358 yk/longsente.test.0<br>   434386 yk/longsente.test.1<br>  2418462 yk/longsente.train.0<br>  7818952 yk/longsente.train.1<br> |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |

|  |  |  |  | CUDA_VISIBLE_DEVICES=0 python python style_transfer_y.py --train ../../data/runtime/yf/sentiment.train.uniq --dev ../../data/runtime/yf/sentiment.dev --test ../../data/runtime/yf/sentiment.test --output ../../data/runtime/aq/04041956 --vocab ../../data/runtime/am/vocab --embedding ../../data/glove.6B.100d.pruned.txt --model ../../data/runtime/aq/04041956.model --dim_emb 100 |
