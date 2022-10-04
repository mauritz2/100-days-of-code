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

