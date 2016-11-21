# Estimating Password Strength

Estimating the strength of a password / passphrase is a daunghting task, converging to the impossible. Relatively you may be able to increase the baseline for the worst passphrases and filter out the most careless offenders, but perfecting it will consume huge amounts of time and bandwidth, and it's one of those problems where you can keep optimizing. You really have to make a strict definition of who your users are in terms of langauge, culture and keyboard, and of course consider your threat model.

## How it's Made®
Password strength is mostly done by estimating the entropy of a given sequence of tokens. What's entropy? It's a measure of chaos. High entropy means something very chaotic or random, while low entropy means something orderly or predictable. So when talking about information, entropy is very closely related to probability. What's tokes? That could be bits, ASCII letters, Unicode code points, words, names, lyrics etc. Essentialy it's where you put the boundary between seperate entities of your "language" or "alphabet". It entirely depends on your perspective.
Since passwords are something you type out on a keyboard and keyboards are come in limited varieties, how the sequence of tokens is generated, ie. typed out, also tells you something about the entropy. Does `juiolk` have high entopy? If you look in a dictionary, yes. Now have a look at your keyboard and take a second guess.
So a strong password is something that has as high entropy as possible. Ideally it's a sequence of tokens from a high entropy source such as `/dev/random` which uses the noise of devices in your computer. However such a sequence doesn't play very nice with the process of comitting to human memory.

## Threat model 
Okay, so if I was an attacker trying to crack passwords by brute-force, how would I go about it? Assuming I did have an idea of the users of the system but didn't know anything about a specific target, apart from a digest of their password, I'd mix of the following:

* Common dictionary
* Common substitiouns
* Common sequences
* Common passwords from leaks
* Cultrual biases; celebreties, dates, superstitions, trivia etc.
* Keyboard layout; pertubations, patterns, available charaters etc.

And this is where you can spent and infinite amount of time, and it essentially becomes an arms race between you and your adversary. You could device an algortihm for each of the subcultures in your user base, but this algorithm would quickly grow large in terms of bytes, given all the data that would have to be encoded in it.

## Password Wars: A New Hope
However when put this way, the problem starts reminiscing of the ways computer vision and computational lingustics used to problem solve; create more and more sophisticated algorthims, hoping to eventually converge on a perfect algorithm. And what are both of these communties doing now? Training Deep Neural Networks on huge swarts of data. And this might be the best solution in 2016. Let a NN read a whole lot of input (Wikimedia, News, random walks on different keyboards, etc.) and then use it to tell you how probable a input sequence was. The advantage here is too that you decide the network size, the network will solve compression at a cost, and can budget accordingly. I'm sure there will be some relevant representation theory or information theory setting the limits of this, but I don't know. 