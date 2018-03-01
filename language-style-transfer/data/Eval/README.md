# OVERVIEW OF THE YELP SET
## CONTENT DISTRIBUTION
Review contents cover: 
* food
* car repair 
* laundry
* salon
* massage
* tattoo

## TYPICAL EXAMPLE
    6
    [Background] came for a family birthday and were seated in the santos room .
    [Comment (good/bad)] the decor and ambiance is nice , the temperature was much too warm with what felt like no ac , just a small electric vertical fan .
    [Comment (good/bad)] the service was mediocre .
    [Comment (good/bad)] took a long time for drink refills or needed to ask more than once .
    [Comment (good/bad)] of our party they forgot to take the order for two people .
    [Comment (good/bad)] chips tasted stale and like old oil , salsa was ok .
    2

## TYPES
### 1. PLAIN NARRATION
*	 i have been getting tattooed by rob @ urban art since _num_ .
*	 has anyone ever had an \`\` eddie murphy '' experience ?
*	 do you remember the movie _num_ hours ?
*	 when eddie murphy goes into the country bar and the music comes to a screeching halt and everyone turns and looks at him ?
*	 i usually get the garden enchiladas .
*	 my wife and i went out of our way to have lunch here .
*	 we stopped here on our way home from golf .
*	 for dinner i was in the mood for a steak so i had the jala holla steak .



### 2. CLEAR & SHALLOW SENTIMENT

####	2.1 EASY 
The sentence is usually like:
STH + is + GOOD/BAD.

		food was amazing !
		we been here a few times and had a positive experience each time .
		love the decor .
		this is our favorite mexican restaurant now .
		yum it was delicious , i will be back for sure !
		our lunch here was really delicious !
		great drinks and apps as well .

####	2.2	CLEAR SENTIMENT, BUT USING COMMONSENSE
The sentence looks neutral, but is not. You need some **commonsense** to understand the sentence.

		i showed up with a friend who is not caucasian , and the bartender did n't acknowledge us at all although we both said hi .
		service was also one step behind denny 's .
		they simply take your order , and bring you good food , followed by the check .
		i will drive out of my way to go here when i 'm in town .
		also , how the hell does a fondue place run out of cheese ? !
		i think this place needs help .
		this place breaks your car so you have to go back to them !
		i 've got to figure out how they made it .
####	2.3 LONG CONTENT + EASY-TO-CONVERT SENTIMENTS
The sentences has some long contents, but clear sentiment expressions of like or dislike. These sentiments are expressed in 1 or 2 adj./ verb./ noun. phrases

		we loved everything we had - guacamole , bean dip , blue seafood enchiladas , crab cake tacos , stacked steak enchilada with an egg , and beef chimichanga .
		i ordered the spooning relleno peppers with cheese and chorizo , breaded and fried , a huge plate with _num_ relleno and rice and beans , very tasty .
		highly recommended - the stacked enchiladas were excellent and the salsa is to die for .
		we had the lobster dip and the garlic shrimp pizza , both were really good .


### 3. INDIRECT SENTIMENT / EUPHEMISTIC (HARD-TO-CONVERT)
These sentiments are hidden in the descriptions. And it's very hard to define an opposite sentence for them.

*	(NEG) they need to take down the sign \`\` ... ... somewhere in the world a vegan is crying ''
*	(NEG) whenever i am seated i always move because they always start placing people nearest to the door and i personally dont like being seated there !
*	(NEG) my tostado looked more like a salad with all the lettuce piled on it .	
*	(NEG) the only thing i would request , is that if the service department is going to be shutting your lights off , please let us know or turn them back on ... .
*	(POS) i 've got to figure out how they made it .
*	(POS) open 24/7 !
*	(NEG) chips tasted stale and like old oil , salsa was ok .
*	(POS) you want a place for a first date ?
*	(POS) ask for sampling before you order though - if you 're going to be drinking that much of one or two flavors , you better make sure it 's a good one .
* (NEG) we have experienced some billing issues ( they overbilled us for a very long time , did n't tell us and just started giving us credits instead of asking if we wanted a refund ) and once they told us that we had no insurance coverage because my _num_ year old reached his lifetime max ( how does that even make sense ? ? ? ? ?



### 4. PARTLY NEG, PARTLY POS
Part of the sentence expresses some sentiment and the other expresses another sentiment.

*	i miss the mario machines they used to have , but it 's still a great place steeped in tradition .
*	i usually order the burger , while the patties are obviously cooked from frozen , all of the other ingredients are very fresh .
*	but other than that the staff is always pleasant and fast to make your order .
*	kind of disappointing ... .but the next day i get a message from the owner/manager apologizing for not calling in advance to make us aware of the closure .
*	now you will spend some money here , but if you really want a special night , this is the place .
*	the actual taste of the dessert was probably the only good thing going however , the restaurant use to offer more of each item of the desserts and when we asked why it changed our waitress explained it was because people would sit for hours upon hours just enjoying dessert asking for more pieces to enjoy their chocolate with .
*	casa reynoso is definitely nothing fancy , but the food is good and consistently so !
*	the service is n't great , but it is more of a hole-in-the-wall so i do n't expect much .
*	service is \`\` eh '' , but the food pretty good .
*	the deep dish pizza is okay ( i had the spinach pie ) , but i think i like uno 's chicago crust better for it 's buttery flakiness ( gasp ! )


## TYPICAL MISTAKES

Quick summary: In order to cover the edge cases for most methods, the evaluation set should include:

* both short and long sentences
* sentences with many adjectives
* sentences with slang expressions, figurative expressions
* sentences with no adj/verb/noun that can be changed into antonyms
* sentences with poor TF-IDF matching
* sentences with lots of objects (food names, service types, etc.)
* sentences with subtle sentiments

### 1. MISTAKES FOR ANTONYM CONVERTION
#### 1.1 Cases where changing to the antonyms doesn't convert the sentiments

	there are only _num_ pumps here and in a small parking lot so good luck trying to maneuver around when its busy .
	it is obvious that ...
#### 1.2 Sentences with too many adjectives
Some of the adjectives should be changed, while others should not.

	i loved when they had the punch card so you got a free coffee after buying so many but now they have an app with lots of deals too which is cool .

#### 1.3 Sentences with no antonyms that WordNet can change
40% of the sentences do not contain words that can be changed into antonyms.

	they also brought my minestrone soup out less than a minute from the time i ordered ( the bus boy overheard my order and left to the kitchen before the waiter ) .
#### 1.4 Limitations of WordNet
* There are phrases that WordNet cannot tackle, such as "less than" -> "more than", "this place is a gem", etc.
* There are inappropriate antonyms that WordNet provides, such as "pretty cool place" -> "ugly warm place", etc.

### 2. MISTAKES FOR TF-IDF
#### 2.1 Long sentences

	but when i went back in they told me they would not replace the order and their policy is you have to bring back the food to get it replaced but none of this was told to me when i called in about the screwed up order and had the name of the person who told me this over the phone and it was even written in their office book for order replacement and they refused to replace the order after making me sit and wait for _num_ minutes just to tell me this .
	was thinking along the lines of a retainer and maybe have to replace the spacers as well but the staff simply told me to hang on while they brought the fork lift out , raised up the rear end , leaned in and twisted in the coils by hand ; also measured the half-to-half on the shocks and recommended a slightly shorter travel if i even wanted to prevent it from happening again ( not that my dw would ever let me get airborne ! ) .
	we initially ordered shutters for _num_ % of our house but once those went in , we ended up ordering for the rest of the house because they were so beautiful ! !
	i 've brought lots of friends and family members with my over the years and every single one has loved it , even those who had no previous experience with thai food .
#### 2.2 Wrong TF-IDF matching
	Original: final price was even a little less than the quote .
	TF-IDF: plus , price was a little less .
	MT: the price was less than the quote .

	Original: i came searching for manapuas ( cha siu ba ) .
	TF-IDF: consistent cha siu and wonton rice noodle soup .
	MT: i came here with a bachelorette party .

#### 2.3 Subtle sentiments:
	i was full from dinner and snuck my drink in .

### 3. MISTAKES FOR STYLE TRANSFER
#### 3.1 Object Mismatch:
	Original: _num_ cent street tacos and the _num_ gordito are amazing .
	Style Transfer: the tacos are $ 4- $ _num_ .

	Original: great food , great service , great beer .
	Style Transfer: terrible service , poor service , horrible food .

#### 3.2 Not accurate at short sentences (compared to Antonym method):
	Original: as i said , best ever !
	Antonym: as i said , worst ever !
	Style Transfer: i 'm so disappointed with my life !

#### 3.3 Not Grammatical, sometimes:
	Original: excellent chinese and superb service .
	Antonym: bad chinese and bad service .
	Style Transfer: terrible food , the food .

	Original: the food is very very amazing like beef and fish .
	Antonym: the food is very very plain like beef and fish .
	Style Transfer: the food was bland and not like the food .
