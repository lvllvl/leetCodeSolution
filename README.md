# leetCodeSolution
#### Writing sample for a LeetCode Medium Solution 

## 1138. Alphabet Board Path
#### Medium

<p align="center">
<img width="403" height="500" src="images/azboard.png">
</p>

Goal: 
We're given a board ( list of alphabet ) and a target ( string ). Our goal is
to document a path from 'a' then to every other letter in target. 

Our starting point is 'a' and our goal is to visit every letter in our target
string. We must document all our movements, which are limited to vertical and
horizontal (no diagonal moves!). 

```
board = [ 'abcde', 'fghij', 'klmno', 'pqrst', 'uvwxy', 'z' ]
target = 'leet'
```
### <ins>Brute Force Solution</ins>
Given the initial data that we're given ( list of strings, a string ), we could
just use that and iterate over the board list continually until we find our
path. This would be unwise mainly because it would require use to continually
iterate over the same string n times, where n in the length of target. 
Using the data given to us and without altering it we can iterate through the
list with a nested for loop. We *could* do that, but our time complexity would
be absurd, since we would need to iterate through the list for every letter in
target.
### ** Insert Time Complexity HERE ** 




### <ins>Hash Map Solution</ins>
To simplify our solution, we should identify our end goals: 
1. We want to find each letter in target
2. We want to track each letter's position in relation to other letters in
  target

We need to reassess the information we need. We need two things to get the
desired output: 
1. We need the letters
2. We need the location of the letters on the board

Now let's combine those pieces of information to be our key : value combination
in our board dictionary. That way we avoid having to loop through the board
list every time we need to find a letter on the board. 
e.g., letter: ( rows, cols )  

<p align="center">
<img width="403" height="500" src="images/azboardCoords.png">
</p>
Here's our updated information: 

```
board = [ 'abcde', 'fghij', 'klmno', 'pqrst', 'uvwxy', 'z' ]
target = 'leet'
b = { 'a': (0,0), 'b':(0,1) ... 'z':(5,0) }
```
Maintaining a dictionary of board coordinates allows us to see where each
letter is in relation to another letter. e.g., 
       ```
       ** Start ** 'a': (0,0)
       ** End ** 'j': (1,4) 
       ```
     To get from 'a' to 'j' we can subtract row2 - row1 and col2 - col1.
     rows = 1 - 0 = 1, cols = 4 - 0 = 4
     Because rows is positive we know that 'j' is one row below 'a', and because cols
     is positive we know that 'j' is four cols to the right of 'a'.

The only thing left to do is to iterate over each letter in target. 

In each example case we are given two clues for how to find a solution. First
we have a list board that contains all alphabetical letters in groups of 5 or
one. Then we have a string target to help us determine which letters to look
for on the board. 

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
b = { 
   board[ word ][ letter ]: for ( word, letter ) for word in range( len(board))
                                       for letter in range( len(board[ word ]) ) 
    }
```

Now that we have a dictionary b, we can access each letter and its coordinates
much faster. 

We can now iterate through the target string letter by letter and compare where
each letter is in comparison to the previous letter. 

