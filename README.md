*Autocomplete* or: How I learned to stop spelling and love our AI overlords
===

---

## To install:

    pip install autocomplete

## How to use:

```python
from autocomplete import autocomplete, models

# load pickled python Counter objects representing our predictive models
# I use Peter Norvigs big.txt (http://norvig.com/big.txt) to create the predictive models
models.load_models()

# imagine writing "the b" 
autocomplete.predict('the','b')

[('blood', 204),
 ('battle', 185),
 ('bone', 175),
 ('best', 149),
 ('body', 149),
 ...]

# now you're typing "the bo"

autocomplete.predict('the','bo')

[('bone', 175),
 ('body', 149),
 ('bones', 122),
 ('boy', 46),
 ('bottom', 32),
 ('box', 24),
 ...]
 
```

If you have your own language model in the form described in [ELI5](#explain-like-im-5), then use the *models* submodule to call the training method:

```python

from autocomplete import models

models.train_models('some giant string of text')

```

Want to run it as a server (bottlepy required)

```python 

import autocomplete

autocomplete.run_server()

#output
Bottle v0.12.8 server starting up (using WSGIRefServer())...
Listening on http://localhost:8080/
Hit Ctrl-C to quit.

```

Now head over to http://localhost:8080/the/bo

```
http://localhost:8080/the/bo
#output
{"body": 149, "box": 24, "bottom": 32, "boy": 46, "borzois": 16, "bodies": 13, "bottle": 13, "bones": 122, "book": 14, "bone": 175}

http://localhost:8080/the/bos
#output
{"boscombe": 11, "boston": 7, "boss": 1, "bosom": 5, "bosses": 4}
```
---

---

Edit*: *To avoid confusion, I wrote this in a the form a letter to my younger siblings.* 

*For Chris, Christine, Mel, and Cat*

## Explain like I'm 5

No. I'm explaining this like you're 5. I know you're not *5* , you guys... Chris, stop jumping on your sister's back!

Ok, so I'm saying, *imagine I'm 5!* 

Oh, that was easy now huh?

Forget the *I'm 5* part. 

Imagine a giant collection of books. 

For example, all the Harry Potter and Hunger Games novels put together. 

What if I asked you to go through all the pages and all the words in those pages? 

Now I'm not asking you four to actually *read* the books. You know, just go through, beginning to end, and notice each word.

For every new word you see, write it down, and put a "1" next to it, and everytime you see a word *again*, add "1" more to the previous number. 

So basically I'm asking y'all to keep count of how many times a word comes up.

Got it? If yes, cool! If not, find a sibling, friend, or adult near you and ask them to help you out :)

...

Say you start with *Harry Potter and the Sorcerer's Stone*:

    Mr. and Mrs. Dursley of number four, Privet Drive, were proud to say that they were perfectly normal, thank you very much...
    
And imagine that you're on the 5th word. This or something close to this is what you're going for:

    Mr.     -> 1
    and     -> 1
    Mrs.    -> 1
    Dursley -> 1
    of      -> 1


Or if you're a *wannabe-Harry-Potter* fan, ah I'm just kidding!   

If you started with *the-book-that-must-not-be-named* - I know you guys won't get it, but persons my age will :)

But I'm sorry, so you started with *The Hunger Games*:

    When I wake up, the other side of the bed is cold...

By the sixth word you have:

    When  -> 1
    I     -> 1
    wake  -> 1
    up    -> 1
    the   -> 1

You have a long day ahead of you...

...

*1,105,285 words later* 

Now that you're done tallying up all those words, why not order all these words by the *number of times you've seen them*? 

Just imagine youstarting from **highest** to **lowest**.

See you next week!

...

Back so soon? You might have something like this:

    psst*, remember, the format is:
     word -> # of times the word appears
    
    'the' -> 80030
    'of'  -> 40025
    'and' -> 38313
    'to'  -> 28766
    'in'  -> 22050
    'a'   -> 21155
    'that'-> 12512
    'he'  -> 12401
    'was' -> 11410
    'it'  -> 10681
    ... there's a lot more words you've tallied up...


Those were the most common words. 

Now on the *less-frequent* end you'll find your words appearing not as often...

    ... 29137 words later.
    'przazdziecka' -> 1
    'disclosure'   -> 1
    'galvanism'    -> 1
    'repertoire'   -> 1
    'bravado'      -> 1
    'gal'          -> 1
    'ideological'  -> 1
    'guaiacol'     -> 1
    'expands'      -> 1
    'revolvers'    -> 1

Yeah Chris? Oh, 'what does lez freken ten' mean? Um, so it means something like: *you probably won't hear or read that word very often.*

Now what if I asked you to help me find this word I'm looking for? And I know this word starts with the letters: 'th'.

This I know you can do much faster! A blazing 5 minutes! IYou did have to go through 29157 unique words after all!


    'the'  -> 80030
    'that' -> 12512
    'this' -> 4063
    'they' -> 3938
    'there'-> 2972
    'their'-> 2955
    'them' -> 2241
    'then' -> 1558
    'these'-> 1231
    'than' -> 1206
    ... 229 words more... 
    

239 words, still kind of lot though huh? And you know your brother, he's too lazy to do this work *by hand* (*cough* programming  *cough*) ;) 

So the word I'm looking for is on the tip of my tongue. I think the next letter is "i".

*1 minute later*

    'this'     -> 4063
    'think'    -> 557
    'things'   -> 321
    'thing'    -> 303
    'third'    -> 239
    'thin'     -> 166
    'thinking' -> 137
    'thirty'   -> 123
    'thick'    -> 77
    'thirds'   -> 43
    ... 36 words more...


*I scan through the first 10 words.* Oh, I just remembered that the next letter is 'r'.

*You start filtering out some more words.*

*10 seconds later.*

    'third'      -> 239
    'thirty'     -> 123
    'thirds'     -> 43
    'thirteen'   -> 32
    'thirst'     -> 13
    'thirteenth' -> 11
    'thirdly'    -> 8
    'thirsty'    -> 5
    'thirtieth'  -> 3
    'thirties'   -> 2

Aha, 'thirdly' was the word I was looking for! What, you never heard of the word "thirdly" before? 

Now you might be saying to yourself, "*that's pretty cool!*", and you're right! 

And you know what's cooler? *Making everyone's life a tiny bit easier* is! :)

But how can you do that with just *words*? 

Aren't words boring and dull? 

It's like all we do is talk, write, and think with *words*. I mean, how lame, I can't even describe to you this *autocomplete* thing-slash-idea-thing without having to write it out with *words*!

Ugh! I hate words! 

*Whoah, wait a minute! That was not cool of me! Let's relax for a minute.* 

Let's try to give an imaginary hug to our word-factory in our brains. That part of our brain works so hard, even when we don't ask it to. How nice of brain to do that. Not! 

Well I guess I should say, sometimes it's not so nice for our brains to distract us, especially when we have homework or other, real-world, problems like adult-homework. 

How about this: try to think about *what* the next sentence coming out of our own mouths *will be*\*. 

Now if you're thinking about what will be coming out of my mouth, or out of your mouth, or your mouth, or your mouth, or your mouth, you're doing it wrong! (to readers who aren't one of my 4 younger siblings, that's how many I got).

Think about *what* the next sentence coming out of *your own* mouth might end up being.

...

Did you decide on your sentence? Good!

What if I asked you to give me just a few reasons explaining *why* or *how* you chose the sentence you chose? 

Wait, I can't even do that. Let's make it easier on ourselves and explain *why* and *how* we chose just the first *word*.

Still pretty hard huh? If you think this part is easy, I'm going to have to say "sorry" and ask you guys to try thinking about it maybe just one more time; this part isn't so easy to ask for help with either :/ 

If you thought about it, and you thought it was pretty darn hard to give a *good and honest* reason as to *why* it is you chose the word you chose, let's bring out a word you guys might not understand: *probability*.

If you feel like you don't *get* what the word means, sure you do! Just use the word "probably" in one of your sentences, but make it kinda makes sense. 

What do I mean? Well, let's just consider the English language. Like most other things, the English language has rules. 

The kind of rules that can be simplified down to: 

1) "***something*** *action* ***something***". 

2) Replace ***something***'s and ***action*** with words that make sense to you.

Fair enough, right? 

Now, imagine you could put *pause* right after the first word that comes out of your mouth.

Let's just say that first word is "the".

Now in the case that you stuttered for reasons outside your conscientious control (for example: "thhh thhe the"). No big deal, you meant to say "the", so let's *flatten* it to just that!

With that *word* said, what words do you *think* you might have said after it? 

You might tell me, "*any word I want!*

Of course you could have! I bet you spent a millisecond thinking about whether or not the next word you were going to say was going to be: *guaiacol*. 

I *know* because I thought about using that word too!

I can remember the first time I heard (or read) *guaiacol* like it was yesterday. I read it in some funky article on the internet. I found the word in a list of words that don't appear too often in the English language.

After I read it, I was able to fit *guaiacol* nicely into that part of my brain where I... uhh.. was... able... uhh...

Oh, you *know*, that place in my brain where I get to choose whether I want to say *the apple*, *the automobile*, *the austronaut*, etc.

...

Ok, so clearly I'm no brain-ician, and that may or may not be the way our brain works - actually, it's probably super super unlikely. 

But even though that idea is probably wrong, the idea itself sounds like a pretty darn good way of suggesting the next word or words somebody is trying to *type*. 

Hey, wait a minute. Where have we seen this before? 

*You google "where you migh..."* Hey! This is where I saw this!

Most search engines of course can do this too you guys.

Oh, silly Google and Microsoft and Yahoo and other giant multi-dollar-naire companies keeping such a cool and useful idea away from us, lol rofl rite!? >.< 

:P 

jaisjdp$4ioj^#asif

92jdfaf 

101

...

Sorry about that.

Ok, let's not lose sight of the much more interesting and useful question we could ask next: *How they do that?!*

Well, turns out you started working on that problem however many minutes it took you, or whoever's reading this to you, to read from the beginning of the article to here!

And we're almost done!

Where were we, like before I got all distracted? 

Turns out 15 sentences ago: "...whether I want to say *the apple*, *the automobile*, *the austronaut*, etc."

What if you had a way to count the number of times you've heard "apple" said after the word "the"? 

Ask yourself the same question, but now with the word "automobile" instead of "apple". 

What if you had the time to think about every possible word that you've ever heard spoken after the word "the"? I'd say it might have looked something like this:

    Words you might have heard following the word "the" and the number of times you might have heard it
    
    'same'     -> 996
    'french'   -> 688
    'first'    -> 652
    'old'      -> 591
    'emperor'  -> 581 
    'other'    -> 528
    'whole'    -> 500
    'united'   -> 466
    'room'     -> 376
    'most'     -> 373
    
    ... 9331 more words...

Not impressed with your brain yet? Let's continue this little thought experiment a little further.

Imagine, you just said "the", and you could put pause after the first *letter* of the next word. 

Real quick, think of the shortest amount of time you can think of. Think of the shortest *second* you can think of. Now shorter than that too. 

At this point, you can't even call that length of time a *second*. But in that length of time, your brain may have just done this:

    'house'   -> 284
    'head'    -> 117
    'hands'   -> 101
    'hand'    -> 97
    'horses'  -> 71
    'hill'    -> 64
    'highest' -> 64
    'high'    -> 57
    'history' -> 56
    'heart'   -> 55

And that brain you got did this realllllyyyyyy fast. Faster than Google, Bing, Yahoo and any other company can ever hope to beat. And your brain did this without even asking for your permission. I think our brains are trying to control us you guys, oh no!

---

###Afterword

notes: \*I have to give a shout out to [Sam Harris](https://twitter.com/SamHarrisOrg) for wonderfully [putting into words](https://www.youtube.com/watch?v=pCofmZlC72g#t=1144) what I've borrowed and slightly adapted for this writing. 

Another shoutout to [Peter Norvig](http://norvig.com) for inspiring me and probably many others with what many will likely consider to be an almost full on copy paste of his [*How to Write a Spell Checker*](http://norvig.com/spell-correct.html)(! But I swear it's not! I actually I think I may have out-Norvig'ed Peter Norvig when it comes to describing [conditional probability](http://en.wikipedia.org/wiki/Conditional_probability): P(wordA & wordB) = P(wordB | wordA)\*P(wordA)

And another one to Rob Renaud's [Gibberish Detector](https://github.com/rrenaud/Gibberish-Detector). I, out of pure chance, ran into his project some time after running into Norvig's article. I can't describe *how* much it helped solidify what the heavy hitters of "AI" consider to be introductory material. 

I can't describe it because I literally *can't* describe it, that is, without me using "likely" and "probably" in what would have likely been every sentence, but who really knows? 

Warning! Second article about this exact thing, only expressed differently, coming soon! Oh and the code too, that is if someone hasn't gotten to translating the above article to code before I can get to uploading the project :P I'm trying to get the kinks out of here and the code so it's simple, duh!

