
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
|  |  |  |  |  |
| ak | 02120842 | att | learning_rate 0.00001 | CUDA_VISIBLE_DEVICES=1 python att.py --train ../data/runtime/ti2/pos2neg/train --vocab ../data/runtime/vocab.txt --embedding ../data/glove.6B.100d.pruned.txt --dev ../data/runtime/ti2/pos2neg/dev --test ../data/runtime/ti2/pos2neg/test --output ../data/runtime/ak/02120842 --model ../data/runtime/at/02090154checkp.ep49.pth.tar --max_epochs 500 --batch_size 1024 --learning_rate 0.00001 |
|  |  |  |  |  |
| at | 02120232 | att | no teacher forcing | CUDA_VISIBLE_DEVICES=2 python
 att.py --train ../data/runtime/ti2/pos2neg/train --vocab ../data/runtime/vocab.txt --embedding ../da
ta/glove.6B.100d.pruned.txt --dev ../data/runtime/ti2/pos2neg/dev --test ../data/runtime/ti2/pos2neg/
test --output ../data/runtime/at/02120232 --model ../data/runtime/at/02090154checkp.ep49.pth.tar --ma
x_epochs 500 --batch_size 1024
 |
