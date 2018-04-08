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
 ```
 regardless of what you order here though , i ca n't imagine it being anything but good , and the cafe is really cute .
had an excellent server , janel .
server ( sasha ) was excellent .
every thursday night they have a free bues concert by hans olson , who is an amazing musician .
the texture ranged from soft to chewy , depending on the size of the piece .
no food , heavy pours , and free pool ... what can be better than that ?
the food is great and they pride themselves on a few house specialities which are standard fare but a cut above the rest or with a unique angle .
notables are their large full wings , but also their dishes with ahi tuna are excellent .
there is n't really proper seating other than a few bar stools at the window but grab your food take it to hunter square and watch a street performer in the sunshine .
ca n't wait until it 's warm enough outside to sit out on the roof deck .
we celebrated our anniversary at oak after hearing amazing reviews following the recent grand opening .
i was staying with a group of friends for a couple of weeks and they told me that i had to go to this bar when them and their friends for trivia .
my only gripe is that i wish there was a bit more quantity in each entree for the price .
were friendly and personable , and our server even went as far as to help us play a joke on a late arriving friend !
love this place : ) awesome decor , nice customer service and yummy poke bowls !
it is a chunky cookie filled with lots of good stuff and tastes like just out of the oven .
i suggested that after 8pm , it should become an adult affair .
for my money , paco 's is the best game in town if you 're craving tex-mex in the queen city .
would have liked to see some more vegetables on the menu besides the few sprigs of garnish .
the most discriminating critic could n't give lola 's less than 4 stars , it really is an exceptional experience in ohio .
everything is delightful but try the tomato fondue thing- you can thank me later : ) the sandwich carvery upstairs is n't too shabby either if you crave something more simple .
i usually get a wrap or a bowl , and they load it up with everything for me .
our awesome waiter informed me that they could accommodate me and the kitchen prepared an incredible veggie dish of broccolini , asparagus , carrots , and marinated mushrooms .
my mom and i came here to eat because we were tanning in the pool area and needed some shade and food .
but u cant go wrong with $ 12.50 buffet dinner where u can have oyster , snow crab legs , sushi and soup .
 ```
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
 * The TF-IDF pairs are _just_ sentences with high cosine similarity of their TF-IDF vectors. It sometimes matches the same sentiment, and not distinguishes contents:
 ```
 the noodles here are really good .
the noodles are good .
the sandwiches for lunch or also highly recommended
tott 's is also really great and highly recommended .
i had the burger which was fantastic .
i had a burger which was very good .
their tortillas are handmade and so fresh and yummy !
you have tasty , handmade tortillas .
 ```
 ** It pays too much attention on modification words
 ```
 again , it is what it , simply great .
it was , simply , ovecooked .
we go there at least once a month because we love their breakfast options !
i used to go there at least once a month .
they were both ridiculously tasty .
ridiculously .
 ```
 * The TF-IDF assigns high similarity to a short sentence which overlaps part of a long sentence. So we constrain the ratio of the longer sentences to the shorter not larger than 1.5
 ```
 not the best but it was affordable and tasted good .
& not affordable .
she 's crafty , she 's gets around she 's crafty , she 's always down she 's crafty , she 's got a gripe she 's crafty , and she 's just my type she 's crafty ... for some reason , when i think of pinspiration , the beastie boys song pops into my head !
& she
i ordered everything with their easy online menu and it was ready for me to pick up at the time specified !
& ordered food for pick up at a specified time .
i had their chicken dish ( forgot what it was called ) , it was a little on the salt side but still edible and full of flavor .
& it was edible with a little flavor .
friendly service , not very noisy .
& very noisy .
 ```
 * But even after the 1.5 length contraint, there are unreasonable ones.
 ```
 desserts : 5 stars macaroons -- 5 stars gelato -- 4.5 stars tiramisu cups -- 4 stars fudge cubes -- 4 stars regular food : 4 stars did n't have as much seafood as i would like .
& the decor - 0 stars the price - 4 stars the service - 3 stars the parking - 2 stars the location - 0 stars the quality 2.5 stars all in all , this place is ok if you 're desperate for a quick hibachi .
 ```
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
