# The Game of Hog

<h2>Introduction</h2>

In this project, you will develop a simulator and multiple strategies for the dice game Hog. You will need to use control statements and higher-order functions together, as described in Sections 1.2 through 1.6 of Composing Programs.

In Hog, two players alternate turns trying to be the first to end a turn with at least 100 total points. On each turn, the current player chooses some number of dice to roll, up to 10. That player's score for the turn is the sum of the dice outcomes.

To spice up the game, we will play with some special rules:

Pig Out. If any of the dice outcomes is a 1, the current player's score for the turn is 1.

Example 1: The current player rolls 7 dice, 5 of which are 1's. They score 1 point for the turn.
Example 2: The current player rolls 4 dice, all of which are 3's. Since Pig Out did not occur, they score 12 points for the turn.
Free Bacon. A player who chooses to roll zero dice scores 2 * tens - ones, or 1, whichever is higher; where tens, ones are the digits of the opponent's score

Example 1: The opponent has 46 points, and the current player chooses to roll zero dice. 2 * 4 - 6 = 2; which is greater than 1, so the current player gains 2 points.
Example 2: The opponent has 73 points, and the current player chooses to roll zero dice. 2 * 7 - 3 = 11; which is greater than 1, so the current player gains 11 points.
Example 3: The opponent has 27 points, and the current player chooses to roll zero dice. 2 * 2 - 7 = -3; which is less than or equal to 1, so the current player gains 1 point.
Example 4: The opponent has 7 points, and the current player chooses to roll zero dice. 2 * 0 - 7 = -7; which is less than or equal to 1, so the current player gains 1 point.
Swine Swap. After points for the turn are added to the current player's score, if the absolute difference between the last two digits of the current score and the last two digits of the opponent's score are the same, the scores are swapped

Hint: recall the built-in function abs which calculates the absolute value of a number

Example 1: The current player has a total score of 41 and the opponent has 83. The current player rolls two dice that total 8. The player's new score is 49, and the opponent's score is 83. The absolute difference between the digits of the current score is |4 - 9| = |-5| = 5; the absolute difference between the digits of the opponent's score is |8 - 3| = |5| = 5. The scores are swapped. The current player now has 83 points and the opponent 49.
Example 2 The current player has a total score of 41 and the opponent has 5. The current player rolls three dice that total 8. The player's new score is 49, and the opponent's score is 5. The absolute difference between the digits of the current score is |4 - 9| = |-5| = 5; the absolute difference between the digits of the opponent's score is |0 - 5| = |-5| = 5. The scores are swapped. The current player now has 5 points and the opponent 49.
Example 3 The current player has a total score of 35 and the opponent has 5. The current player rolls three dice that total 8. The player's new score is 43, and the opponent's score is 5. The absolute difference between the digits of the current score is |4 - 3| = |1| = 1; the absolute difference between the digits of the opponent's score is |0 - 5| = |5| = 5. The scores are not swapped. The current player now has 43 points and the opponent still has 5.
Example 4 The current player has a total score of 0 and the opponent has 0. The current player rolls three dice that total 11. The player's new score is 11, and the opponent's score is 0. The absolute difference between the digits of the current score is |1 - 1| = |0| = 0; the absolute difference between the digits of the opponent's score is |0 - 0| = |0| = 0. The scores are swapped. The current player now has 0 points and the opponent 11

A graphical user interface (GUI, for short) is provided for you. At the moment, it doesn't work because you haven't implemented the game logic. Once you complete the play function, you will be able to play a fully interactive version of Hog!

In order to render the graphics, make sure you have Tkinter, Python's main graphics library, installed on your computer. Once you've done that, you can run the GUI from your terminal:

python3 hog_gui.py

Once you complete the project, if you completed the optional Problem 12, you can play against the final strategy that you've created!

python3 hog_gui.py -f

Phase 1: Simulator

Problem 0 (0 pt)
The dice.py file represents dice using non-pure zero-argument functions. These functions are non-pure because they may have different return values each time they are called. The documentation of dice.py describes the two different types of dice used in the project:

Dice can be fair, meaning that they produce each possible outcome with equal probability. Example: six_sided.
For testing functions that use dice, deterministic test dice always cycle through a fixed sequence of values that are passed as arguments to the make_test_dice function.
Before we start writing any code, read over the dice.py file and check your understanding by unlocking the following tests.

python3 ok -q 00 -u

You should type in what you expect the output to be. To do so, you need to first figure out what test_dice will do, based on the description above.

You can exit the unlocker by typing exit() (without quotes). Typing Ctrl-C on Windows to exit out of the unlocker has been known to cause problems, so avoid doing so.

<h3> Problem 1 (2 pt)</h3>

Implement the roll_dice function in hog.py. It takes two arguments: a positive integer called num_rolls giving the number of dice to roll and a dice function. It returns the number of points scored by rolling the dice that number of times in a turn: either the sum of the outcomes or 1 (Pig Out).

To obtain a single outcome of a dice roll, call dice(). You should call dice() exactly num_rolls times in the body of roll_dice. Remember to call dice() exactly num_rolls times even if Pig Out happens in the middle of rolling. In this way, we correctly simulate rolling all the dice together.

Understand the problem:

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 01 -u
Write code and check your work:

Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 01
Debugging your code interactively:

If the tests don't pass, it's time to debug. You can observe the behavior of your function using Python directly. First, start the Python interpreter and load the hog.py file.

python3 -i hog.py
Then, you can call your roll_dice function on any number of dice you want. The roll_dice function has a default argument value for dice that is a random six-sided dice function. Therefore, the following call to roll_dice simulates rolling four fair six-sided dice.

>>> roll_dice(4)
You will find that the previous expression may have a different result each time you call it, since it is simiulating random dice rolls. You can also use test dice that fix the outcomes of the dice in advance. For example, rolling twice when you know that the dice will come up 3 and 4 should give a total outcome of 7.

>>> fixed_dice = make_test_dice(3, 4)
>>> roll_dice(2, dice=fixed_dice)
7
On most systems, you can evaluate the same expression again by pressing the up arrow or Control-P, then pressing enter or return.

If you find a problem, you need to change your hog.py file, save it, quit Python, start it again, and then start evaluating expressions. Pressing the up arrow should give you access to your previous expressions, even after restarting Python.

Continue debugging your code and running the ok tests until they all pass. You should follow this same procedure of understanding the problem, implementing a solution, testing, and debugging for all the problems on this project.

<h3> Problem 2 (1 pt)</h3>

Implement the free_bacon helper function that returns the number of points scored by rolling 0 dice, based on the opponent's current score. You can assume that score is less than 100. For a score less than 10, assume that the first of the two digits is 0.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 02 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 02
As noted above, you can also test free_bacon interactively by entering python3 -i hog.py in the terminal and then calling free_bacon with various inputs.

<h3> Problem 3 (2 pt)</h3>

Implement the take_turn function, which returns the number of points scored for a turn by rolling the given dice num_rolls times.

You will need to implement the Free Bacon rule based on opponent_score, which you can assume is less than 100.

Your implementation of take_turn should call both roll_dice and free_bacon when possible.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 03 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 03

<h3> Problem 4 (1 pt)</h3>

Implement is_swap, which returns whether or not the scores should be swapped because the difference between the last two digits of the current player's score is the same as the difference between the last two digits of the opponent's score.

The is_swap function takes two arguments: the players' scores. It returns a boolean value to indicate whether the Swine Swap condition is met.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 04 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 04

<h3> Problem 5 (2 pt)</h3>

Implement the play function, which simulates a full game of Hog. Players alternate turns rolling dice until one of the players reaches the goal score.

To determine how much dice are rolled each turn, each player uses their respective strategy (Player 0 uses strategy0 and Player 1 uses strategy1). A strategy is a function that, given a player's score and their opponent's score, returns the number of dice that the current player wants to roll in the turn. Each strategy function should be called only once per turn. Don't worry about the details of implementing strategies yet. You will develop them in Phase 3.

When the game ends, play returns the final total scores of both players, with Player 0's score first, and Player 1's score second.

Here are some hints:

You should use the functions you have already written! You will need to call take_turn with all three arguments.
Only call take_turn once per turn.
Enforce all the special rules.
You can get the number of the other player (either 0 or 1) by calling the provided function other.
You can ignore the say argument to the play function for now. You will use it in Phase 2 of the project.
Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 05 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 05
The last test for Question 5 is a fuzz test, which checks that your play function works for a large number of different inputs. Failing this test means something is wrong, but you should look at other tests to see where the problem might be.

Once you are finished, you will be able to play a graphical version of the game. We have provided a file called hog_gui.py that you can run from the terminal:

python3 hog_gui.py
If you don't already have Tkinter (Python's graphics library) installed, you'll need to install it first before you can run the GUI.

The GUI relies on your implementation, so if you have any bugs in your code, they will be reflected in the GUI. This means you can also use the GUI as a debugging tool; however, it's better to run the tests first.

Make sure to submit by the earlier deadline using the following command

python3 ok --submit
Congratulations! You have finished Phase 1 of this project!

Phase 2: Commentary

Important submission note: For full credit:

submit with Phase 2 and 3 complete by Thursday, September 6.
You will get an extra credit point for submitting the entire project at least 24 hours early.

You can work on and submit Phase 2 and 3 with a partner! Make sure one of you submits and then lists the other as a partner on okpy.org

In the second phase, you will implement commentary functions that print remarks about the game after each turn, such as, "22 points! That's the biggest gain yet for Player 1."

A commentary function takes two arguments, Player 0's current score and Player 1's current score. It can print out commentary based on either or both current scores and possibly even previous scores. Since commentary can differ from turn to turn depending on the current point situation in the game, commentary functions return another commentary function to be called on the next turn. The only side effect of a commentary function should be to print.

Commentary examples
The function say_scores in hog.py is an example of a commentary function that simply announces both players' scores. Note that say_scores returns a reference to itself, meaning that the same commentary function will be called each turn.

def say_scores(score0, score1):
    """A commentary function that announces the score for each player."""
    print("Player 0 now has", score0, "and Player 1 now has", score1)
    return say_scores
The function announce_lead_changes is an example of a higher-order function that returns a commentary function that tracks lead changes.

def announce_lead_changes(previous_leader=None):
    """Return a commentary function that announces lead changes.

    >>> f0 = announce_lead_changes()
    >>> f1 = f0(5, 0)
    Player 0 takes the lead by 5
    >>> f2 = f1(5, 12)
    Player 1 takes the lead by 7
    >>> f3 = f2(8, 12)
    >>> f4 = f3(8, 13)
    >>> f5 = f4(15, 13)
    Player 0 takes the lead by 2
    """
    def say(score0, score1):
        if score0 > score1:
            leader = 0
        elif score1 > score0:
            leader = 1
        else:
            leader = None
        if leader != None and leader != previous_leader:
            print('Player', leader, 'takes the lead by', abs(score0 - score1))
        return announce_lead_changes(leader)
    return say
You should also understand the function both, which takes two commentary functions (f and g) and returns a new commentary function. This returned commentary function returns another commentary function which calls the functions returned by calling f and g, in that order.

def both(f, g):
    """Return a commentary function that says what f says, then what g says.

    >>> h0 = both(say_scores, announce_lead_changes())
    >>> h1 = h0(10, 0)
    Player 0 now has 10 and Player 1 now has 0
    Player 0 takes the lead by 10
    >>> h2 = h1(10, 6)
    Player 0 now has 10 and Player 1 now has 6
    >>> h3 = h2(6, 17) # Player 0 gets 7 points, then Swine Swap applies
    Player 0 now has 6 and Player 1 now has 17
    Player 1 takes the lead by 11
    """
    def say(score0, score1):
        return both(f(score0, score1), g(score0, score1))
    return say
    
<h3> Problem 6 (2 pt)</h3>

Update your play function so that a commentary function is called at the end of each turn. The return value of calling a commentary function gives you the commentary function to call on the next turn.

For example, say(score0, score1) should be called at the end of the first turn. Its return value (another commentary function) should be called at the end of the second turn. Each consecutive turn, call the function that was returned by the call to the previous turn's commentary function.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 06 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 06

<h3> Problem 7 (3 pt)</h3>

Implement the announce_highest function, which is a higher-order function that returns a commentary function. This commentary function announces whenever a particular player gains more points in a turn than ever before. To compute the gain, it must compare the score from last turn to the score from this turn for the player of interest, which is designated by the who argument. This function must also keep track of the highest gain for the player so far.

The way in which announce_highest announces is very specific, and your implementation should match the doctests provided. Don't worry about singular versus plural when announcing point gains; you should simply use "point(s)" for both cases.

Hint. The announce_lead_changes function provided to you is an example of how to keep track of information using commentary functions. If you are stuck, first make sure you understand how announce_lead_changes works.


Hint. The doctests for both/announce_highest in hog.py might be outdated, describing a game that may be impossible under the current rules. This shouldn't be an issue for commentary functions since they don't implement any of the rules of the game


Hint. If you're getting a local variable [var] reference before assignment error:

This happens because in Python, you aren't normally allowed to modify variables defined in parent frames. Instead of reassigning [var], the interpreter thinks you're trying to define a new variable within the current frame. We'll learn about how to work around this in a future lecture, but it is not required for this problem.

To fix this, you can either:

1) Rather than reassigning [var] to its new value, create a new variable to hold that new value. Use that new variable in future calculations.

2) For this problem specifically, avoid this issue entirely by not modifying/defining additional variables and instead using a built-in function to calculate your desired value when creating the new commentary function.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 07 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 07
When you are done, if play the game again, you will see the commentary.

python3 hog_gui.py
The commentary in the GUI is generated by passing the following function as the say argument to play.

both(announce_highest(0), both(announce_highest(1), announce_lead_changes()))
Great work! You just finished Phase 2 of the project!

Phase 3: Strategies
In the third phase, you will experiment with ways to improve upon the basic strategy of always rolling a fixed number of dice. First, you need to develop some tools to evaluate strategies.

<h3> Problem 8 (2 pt) </h3>

Implement the make_averaged function, which is a higher-order function that takes a function fn as an argument. It returns another function that takes the same number of arguments as fn (the function originally passed into make_averaged). This returned function differs from the input function in that it returns the average value of repeatedly calling fn on the same arguments. This function should call fn a total of num_samples times and return the average of the results.

To implement this function, you need a new piece of Python syntax! You must write a function that accepts an arbitrary number of arguments, then calls another function using exactly those arguments. Here's how it works.

Instead of listing formal parameters for a function, we write *args. To call another function using exactly those arguments, we call it again with *args. For example,

>>> def printed(fn):
...     def print_and_return(*args):
...         result = fn(*args)
...         print('Result:', result)
...         return result
...     return print_and_return
>>> printed_pow = printed(pow)
>>> printed_pow(2, 8)
Result: 256
256
>>> printed_abs = printed(abs)
>>> printed_abs(-10)
Result: 10
10
Read the docstring for make_averaged carefully to understand how it is meant to work.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 08 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 08

<h3> Problem 9 (2 pt)</h3>

Implement the max_scoring_num_rolls function, which runs an experiment to determine the number of rolls (from 1 to 10) that gives the maximum average score for a turn. Your implementation should use make_averaged and roll_dice.

If two numbers of rolls are tied for the maximum average score, return the lower number. For example, if both 3 and 6 achieve a maximum average score, return 3.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 09 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 09
To run this experiment on randomized dice, call run_experiments using the -r option:

python3 hog.py -r
Running experiments For the remainder of this project, you can change the implementation of run_experiments as you wish. By calling average_win_rate, you can evaluate various Hog strategies. For example, change the first if False: to if True: in order to evaluate always_roll(8) against the baseline strategy of always_roll(4). You should find that it wins slightly more often than it loses, giving a win rate around 0.5.

Some of the experiments may take up to a minute to run. You can always reduce the number of samples in make_averaged to speed up experiments.

<h3> Problem 10 (1 pt)</h3>

A strategy can take advantage of the Free Bacon rule by rolling 0 when it is most beneficial to do so. Implement bacon_strategy, which returns 0 whenever rolling 0 would give at least margin points and returns num_rolls otherwise.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 10 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 10
Once you have implemented this strategy, change run_experiments to evaluate your new strategy against the baseline. You should find that it wins more than half of the time.

<h3> Problem 11 (2 pt)</h3>

A strategy can also take advantage of the Swine Swap rule. The swap_strategy rolls 0 if it would cause a beneficial swap. It also returns 0 if rolling 0 would give at least margin points, unless this would cause a non-beneficial swap. Otherwise, the strategy rolls num_rolls.

Before writing any code, unlock the tests to verify your understanding of the question.

python3 ok -q 11 -u
Once you are done unlocking, begin implementing your solution. You can check your correctness with:

python3 ok -q 11
Once you have implemented this strategy, update run_experiments to evaluate your new strategy against the baseline. You should find that it gives a significant edge over always_roll(4).

<h3> Optional: Problem 12 (0 pt)</h3>

Implement final_strategy, which combines these ideas and any other ideas you have to achieve a high win rate against the always_roll(4) strategy. Some suggestions:

swap_strategy is a good default strategy to start with.
There's no point in scoring more than 100. Check whether you can win by rolling 0, 1 or 2 dice. If you are in the lead, you might take fewer risks.
Try to force a beneficial swap.
Choose the num_rolls and margin arguments carefully.
You can check that your final strategy is valid by running Ok.

python3 ok -q 12
You can also check your exact final winrate by running

python3 calc.py
At this point, run the entire autograder to see if there are any tests that don't pass.

python3 ok
Once you are satisfied, submit to Ok to complete the project.

python3 ok --submit
If you have a partner, make sure to add them to the submission on okpy.org.

You can also play against your final strategy with the graphical user interface:

python3 hog_gui.py -f
The GUI will alternate which player is controlled by you.

Congratulations, you have reached the end of your first CS 61A project! If you haven't already, relax and enjoy a few games of Hog with a friend.
