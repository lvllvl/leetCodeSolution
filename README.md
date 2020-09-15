# leetCodeSolution
#### Writing sample for a LeetCode Medium Solution 

## 1138. Alphabet Board Path
#### Medium

<p align="center">
<img width="403" height="500" src="images/azboard.png">
</p>

As the title suggests we should think of the alphabet as a board. We use the
string target as a reference for the letters we need to find in the list board. 

### <ins>Goal:</ins> 
We are given a visual representation of the board (above) and a list
representation of board (below). 

```
board = [ 'abcde', 'fghij', 'klmno', 'pqrst', 'uvwxy', 'z' ]
target = 'leet'
```
Starting at 'a' our goal is to find every letter on the board. We will track 
our movement as we move along the board, i.e., we are tracking each letter in
target and the path to the next letter in target. 


<ins>Example 1:</ins> 
```
Input: target = "leet"
Output: "DDR!UURRR!!DDD!"
```

## <ins>Brute Force Solution</ins>

As the data is currently formatted, we would need to continually loop through
the board list. So for every letter in target we need to loop one time. 

A worst case scenario for this is that target length is 100 and that every
letter in target is 'z'.  
### ** Insert Time Complexity HERE ** 

<br>


## <ins>Better Solution</ins>
The bottle neck in the previous example appeared because we tried to access the
letters using the board list. We need to find an alternative data structure
that allows us to:
- Access letter quickly 
- Access each letter's position in relation to other letters

Re-imagine the alphabet board so that every letter contains coordinates, as
shown in the image below. 

<p align="center">
<img width="403" height="500" src="images/azboardCoords.png">
</p>

A dictionary allows us to organize our alphabet board in a way that meets our
data structure requirements. The lookup time for a dictionary is O( 1 ) and we
can pair our letters with their coordinates on the board, e.g., 'a': (0,0),
'b': (0,1), etc.
Let's create a dictionary comprehension to create our new board dictionary. 

```
new_board = { board[word][letter]: (word,letter) for word in range(len(board))
                                             for letter in range(len(board[word])) }
```

### *How do we use our dictionary to solve our problem?*

Here's a quick example for how we will use our dictionary. If target = 'aj' our
task is to record the directions we need to take from 'a' in order to arrive at 'j'.

```
Start at 'a': (0,0)
End at 'j': (1,4) 

Up / Down formula --> row2 - row1 = vertical movment 
Left / Right formula --> col2 - col1 = horizontal movement 

verticalMovment = 1 - 0 = 1 -> one down
horizontalMovement = 4 - 0 = 4 -> four to the right 

output:'DRRRR!'
```
In the example we developed a formula for finding directions between letters. Now let's convert that into some code. 
```
def calculate( curr, dest ):
   currRow, currCol = curr # We can unpack our tuples this way
   destRow, destCol = dest 

   row = destRow - currRow
   col = destCol - currCol 

   return row, col 
```


