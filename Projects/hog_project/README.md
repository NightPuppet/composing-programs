
### Introduction

This [project](https://inst.eecs.berkeley.edu//~cs61a/fa13/proj/hog/hog.html), you will develop a simulator and multiple strategies for the dice game Hog. You will need to use control and higher-order functions together, from Sections 1.1 through 1.6 of the [Composing Programs](http://composingprograms.com/pages/11-getting-started.html) online text.

In Hog, two players alternate turns trying to reach 100 points first. On each turn, the current player chooses some number of dice to roll, up to 10. Her turn score is the sum of the dice outcomes, unless any of the dice come up a 1, in which case the score for her turn is only 1 point (the **Pig out** rule).

To spice up the game, we will play with some special rules:

1. **Free bacon**. If a player chooses to roll zero dice, she scores one more than the largest digit in her opponent's score. For example, if Player 1 has 42 points, Player 0 gains 1 + max(4, 2) = 5 points by rolling zero dice. If Player 1 has 48 points, Player 0 gains 1 + max(4, 8) = 9 points.
2. **Hog wild**. If the sum of both players' total scores is a multiple of seven (e.g., 14, 21, 35), then the current player rolls four-sided dice instead of the usual six-sided dice.
3. **Swine swap**. If at the end of a turn one of the player's total score is exactly double the other's, then the players swap total scores. *Example 1:* Player 0 has 20 points and Player 1 has 5; it is Player 1's turn. She scores 5 more, bringing her total to 10. The players swap scores: Player 0 now has 10 points and Player 1 has 20. It is now Player 0's turn. *Example 2*: Player 0 has 90 points and Player 1 has 50; it is Player 0's turn. She scores 10 more, bringing her total to 100. The players swap scores, and Player 1 wins the game 100 to 50.

### Problems I solved

**Problem 1**  Implement the roll_dice function in hog.py, which returns the number of points scored by rolling a fixed positive number of dice: either the sum of the dice or 1. To obtain a single outcome of a dice roll, call dice(). You should call this function exactly num_rolls times in your implementation. The only rule you need to consider for this problem is Pig out.

**Problem 2** Implement the take_turn function, which returns the number of points scored for the turn. You will need to implement the Free bacon rule here. You can assume that opponent_score is less than 100. Your implementation should call roll_dice.

**Problem 3** Implement select_dice, a helper function that will simplify the implementation of play (next problem). The function select_dice helps enforce the Hog wild special rule. This function takes two arguments: the scores for the current and opposing players.

**Problem 4** Finally, implement the play function, which simulates a full game of Hog. Players alternate turns, each using the strategy originally supplied, until one of the players reaches the goal score. When the game ends, play returns the final total scores of both players, with Player 0's score first, and Player 1's score second.

**Problem 5** Implement the make_averaged function. This higher-order function takes a function fn as an argument. It returns another function that takes the same number of arguments as the original. This returned function differs from the input function in that it returns the average value of repeatedly calling fn on the same arguments. This function should call fn a total of num_samples times and return the average of the results.

**Problem 6** Implement the max_scoring_num_rolls function, which runs an experiment to determine the number of rolls (from 1 to 10) that gives the maximum average score for a turn. Your implementation should use make_averaged and roll_dice. It should print out the average for each possible number of rolls, as in the doctest for max_scoring_num_rolls.

**Problem 7** A strategy can take advantage of the Free bacon rule by rolling 0 when it is most beneficial to do so. Implement bacon_strategy, which returns 0 whenever rolling 0 would give at least BACON_MARGIN points and returns BASELINE_NUM_ROLLS otherwise (these two global variables are located right above the always_roll function).

**Problem 8** A strategy can also take advantage of the Swine swap rule. Implement swap_strategy, which
1. Rolls 0 if it would cause a beneficial swap that gains points.
2. Rolls BASELINE_NUM_ROLLS if rolling 0 would cause a harmful swap that loses points.
3. If rolling 0 would not cause a swap, then do so if it would give at least BACON_MARGIN points and roll BASELINE_NUM_ROLLS otherwise.

**Problem 9** Implement final_strategy, which combines these ideas and any other ideas you have to achieve a win rate of at least 0.59 against the baseline always_roll(5) strategy.

### My note

Every problem has passed internal tests which can be done through:
```
python3 hog_grader.py -q i
where i - number of problem
```
final_strategy win rate: 0.592155 (done on 100000 tests)

