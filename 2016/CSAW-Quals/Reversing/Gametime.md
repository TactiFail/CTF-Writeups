**Points:** 50

Not proud of this one, but it worked.  The game is basically like Dance Dance Revolution, but with the space bar, X, and M.  When you see S, you type the space bar, and when you see X or M you press that key.

Well, it can get kinda fast at points, so my first thought was to write something to read out the keys and play them back really fast.  During testing however I noticed two things:

1. The pattern never changes
2. The keys you enter are stored in a buffer and one is grabbed each time it needs a character of input

So basically, since the first few are always `SXM`, I typed those in one after another before the game even asked for input, and it accepted them all when needed.  From there it was just a matter of getting as far as I could, writing down the pattern, and typing it in at the beginning.

Not elegant by any means, but it worked.

The pattern is:

`sxmsxmmxsmmxxmxssxm`

And then eventually you find the flag:

`no5c30416d6cf52638460377995c6a8cf5`

There was actually some output after the flag, but I was more interested in attacking other challenges than continuing down this rabbit hole  :)
