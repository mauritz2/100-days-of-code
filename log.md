# 100 Days Of Code - Log

### Day 0: October 1, 2022

**Today's Progress**: Added test cases for the determine winner function in Arboretum and added the graveyard class 

**Thoughts:** This was interesting: https://stackoverflow.com/questions/33533148/how-do-i-type-hint-a-method-with-the-type-of-the-enclosing-class
How to do type hints when you're type hinting the class itself. Tried the from __ future __ import annotations solution, but it threw an error.
Seems like it messed up how the Player class was being interpreted in an unexpected way. Would like to understand what __future__is better

**Project** https://github.com/mauritz2/arboretum

### Day 1: October 2, 2022

**Today's Progress**: Added the Game Manager to Arboretum and started implementing its logic

**Thoughts:** Realizing it's best to implement even very simple methods for classes, to reduce coupling.
E.g. I know the deck is a list of cards, so to get the top card I could do [-1]. But if I change it so that the top card is now [0],
or I change cards to be a dict I now have to change both the Deck class, AND where I referenced [-1]. So better that
the Deck class has a method called get_top_card() to abstract how it actually gets that card.

**Project** https://github.com/mauritz2/arboretum

### Day 2: October 3, 2022

**Today's Progress**: Finalized a first version of the complete Arboretum game logic

**Thoughts:** Feels good to put all the pieces together finally. There's more clean-up to be done (e.g. allowing for draws, refactoring,
making it more clear what paths scored points). But main thing would be to build a front-end for this logic that can be interacted with.
I'd probably turn it into a Flask app. TBD.

**Project** https://github.com/mauritz2/arboretum

### Day 3: October 4, 2022

**Today's Progress**: Took a first pass at turning Arboretum into a web app

**Thoughts:** Found a six-year-old Flask app that implemented Hearts that I'll use as a base for building Arboretum into a web app :-) https://github.com/rohanil/hearts
The original ambition was to make the cards draggable, but seems easier to start with just having a "Play" button per card that hide/show based on whose turn it is
Found out about Miniconda - it works well, I can manage envs there without having to install full Conda https://docs.conda.io/en/latest/miniconda.html

**Project** https://github.com/mauritz2/arboretum

### Day 4: October 5, 2022

**Today's Progress**: Updated the web app so that it can display a player's hand

**Thoughts:** Brushing up on some Bootstrap and CSS. "Col" without anything means Col-1. To introduce bottom padding do "pb-x" where x is the bottom padding.

**Project** https://github.com/mauritz2/arboretum

### Day 5: October 6, 2022

**Today's Progress**: Continued on the web app - rendering the board and first pass at being able to choose a card and then play it to the board

**Learnings:**
* CSS cares about spaces .table : hover didn't work, but .table:hover works,
* Margin controls the space OUTSIDE an element, padding controls the space INSIDE an element. I always tend to use padding, but should be using more margin since that's most often what I need to change
* Fun Flask issue to troubleshoot: the web app wouldn't update. The issue was that PyCharm was running the main() which was also running Flask. Stopping that caused the app to start refreshing again.

**Project** https://github.com/mauritz2/arboretum

### Day 6: October 7, 2022

**Today's Progress**: Followed a tutorial on how to set up a simple API using Flask (https://auth0.com/blog/developing-restful-apis-with-python-and-flask/#-span-id--flask-on-docker----span--Dockerizing-Flask-Applications)

**Learnings:**
* The timeit Python module can be used to test performance on short snippets of code, e.g.: python -m timeit '"-".join(str(n) for n in range(100))'. This is cool. When I tried to time some code earlier both options executed too quickly to see the difference in the execution time, but timeit can execute it 1000s of times to spot the difference. 
* Windows doesn't have a wget or curl equivalent. But a Windows-version of Wget can be downloaded to Windows and copied into System32 and it works. Very convenient.
* "export" equivalent on windows is "set"
* flask run looks for the env variable FLASK_APP and will try to run it - if you set that env variable and flask run the app will run
* wget -O- outputs the output directly in the console as opposed to a file, saves time. O stands for output and the subsequent - indicates the console is the output.