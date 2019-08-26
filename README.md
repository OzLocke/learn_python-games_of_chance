-   [Define the variables](#define-the-variables)
-   [Define utility functions](#define-utility-functions)
-   [Define the games](#define-the-games)
    -   [Coin Toss](#coin-toss)
    -   [Cho Han](#cho-han)
-   [Play the games!](#play-the-games)
    -   [The Coin Toss game](#the-coin-toss-game)
    -   [The Cho-Han game](#the-cho-han-game)

Define the variables
====================

Here we establish the global variables for the project, and load any
packages needed

``` python
#--INITIALISE--#
import random
denomination = "chips"
wallet = 100
```

Define utility functions
========================

Here we establish functions that will be used only by other functions.

The print\_result function outputs the result of any game function,
adding information about the player’s remaining balance. Although it’s
only a single line of code, I chose to make it a utility function so I
can change the layout of the output display in one place.

``` python
#--DEFINE UTILITY FUNCTIONS--#
def print_result(result):
    # Output result
    print(result + "\n\nYou have " + str(wallet) + " " + denomination + " left.")
```

Define the games
================

Coin Toss
---------

The Coin Toss game takes a pot (the amount the player bets) as an
integer and a call as either heads or tails.

1.  The two possible call values are asigned to a list called
    **outcomes** so that we can (using *list*.index) view the call as
    either a string or an integer
2.  Assign a random int between 0 and 1 for the result of the **toss**
    (heads and tails respectively)
3.  Find the string version of the **toss** result by using the **toss**
    result as the index for returning a value from the **outcomes** list
4.  Convert the original **call** value to an integer by looking up the
    string value in the **outcomes** list and returning it’s posision
    (with *list*.index)
5.  Process the result of the game…
    1.  Populate the **result** value based on the comparing **toss** to
        **call**
    2.  Adjust the **wallet** *global* variable by the pot accordingly
6.  Pass the **result** of the game to the **print\_result** function to
    display it

``` python
#--DEFINE GAME FUNCTIONS--#
# Coin Toss
def coin_toss(pot, call):
    # Define variables
    global wallet
    outcomes = ["heads", "tails"]
    toss = random.randint(0,1)
    toss_string = outcomes[toss]
    call = outcomes.index(call)
    
    # Find result
    if call == toss:
        result = toss_string + "\n\nYou guessed correctly!\n\nYou won " + str(pot) + " " + denomination + "!"
        wallet += pot
    else:
        result = toss_string + "\n\nYou guessed incorrectly.\n\nYou lost " + str(pot) + " " + denomination + "."
        wallet -= pot

    # Output result
    print_result(result)
```

Cho Han
-------

The Cho Han game takes a pot (the amount the player bets) as an integer
and a call as either even or odd.

1.  The two possible call values are asigned to a list called
    **outcomes** so that we can (using *list*.index) view the call as
    either a string or an integer
2.  Assign a random int between 0 and 1 for the result of the **roll**
    (even and odd respectively)
3.  Find the string version of the **roll** result by using the **roll**
    result as the index for returning a value from the **outcomes** list
4.  Convert the original **call** value to an integer by looking up the
    string value in the **outcomes** list and returning it’s posision
    (with *list*.index)
5.  Process the result of the game…
    1.  Populate the **result** value based on the comparing **roll** to
        **call**
    2.  Adjust the **wallet** *global* variable by the pot accordingly
6.  Pass the **result** of the game to the **print\_result** function to
    display it

``` python
# Cho-Han
def cho_han(pot, call):
    # Define variables
    global wallet
    outcomes = ["even", "odd"]
    roll = random.randint(1,6) + random.randint(1,6)
    roll_type = roll % 2
    roll_string = outcomes[roll_type]
    call = outcomes.index(call)

    # Find result
    if call == roll_type:
        result = str(roll) + "... " + roll_string + "\n\nYou guessed correctly!\n\nYou won " + str(pot) + " " + denomination + "!"
        wallet += pot
    else:
        result = str(roll) + "... " + roll_string + "\n\nYou guessed incorrectly.\n\nYou lost " + str(pot) + " " + denomination + "."
        wallet -= pot
    
    # Output result
    print_result(result)
```

Play the games!
===============

The Coin Toss game
------------------

Call the game!

``` python
#--CALL GAMES--#
# Coin Toss
coin_toss(20, "heads")
```

    ## heads
    ## 
    ## You guessed correctly!
    ## 
    ## You won 20 chips!
    ## 
    ## You have 120 chips left.

The Cho-Han game
----------------

Call the game!

``` python
# Cho-Han
cho_han(20, "odd")
```

    ## 7... odd
    ## 
    ## You guessed correctly!
    ## 
    ## You won 20 chips!
    ## 
    ## You have 140 chips left.
