# leetCodeSolution
#### Writing sample for a LeetCode Medium Solution 

## 1138 Medium - 

<p align="center">
<img width="375" height="300" src="images/azboard.png">
</p>

In the initial example they provide us with the clue that the alphabet should
be treated as a board.

In each example case we are given two clues for how to find a solution. First
we have a list board that contains all alphabetical letters in groups of 5 or
one. Then we have a string target to help us determine which letters to look
for on the board. 

```
board = [ 'abcde', 'fghij', 'klmno', 'pqrst', 'uvwxy', 'z' ]
target = 'leet'

```

Our starting point will always be 'a'. We could use board as it is but what if
the first letter of target is 'z' and the next letter is 'a' again? To traverse
this list over and over will increase the time complexity unnecessarily. But
how should we store this board of letters? 

We want a data structure that helps us maintain a board structure and also
helps us to access each element quickly. A good alternative would be a
dictionary. 

The trick with a dictionary is to develop the best key, value pairing that best
suits your solution. In our case, our goal is to find where each letter on the
board relative to other letters on the board. So in other words we need letters
and letter positions ( i.e., letters : letter coordinates ). 

Let's take the board we've been given initially and convert by using a
dictionary comprehension. 
```
b = { board[ word ][ letter ]: for ( word, letter ) for word in range( len(
board ) )
for letter in range( len( board[ word ] ) ) }

```
