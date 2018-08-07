# Katas Library
This readme contain varying katas to practice. Listed below each set of instructions is my own initial solution to the problem.

<h2 align="center">Unique Order</h2>
<h3>Instructions</h3>

Implement the function unique_in_order which takes as argument a sequence and returns a list of items without any elements with the same value next to each other and preserving the original order of elements.

```
test.assert_equals(unique_in_order('AAAABBBCCDAABBB'), ['A','B','C','D','A','B'])
```

<h3>Solution</h3>

```
def unique_in_order(iterable):
    last = None
    output_list = []
    
    for char in iterable:
        if char != last:
            output_list.append(char)
            print('char: {}'.format(char))
        last = char
    
    return output_list
```

<h2>Build Tower</h2>
<h3>Instructions</h3>

Build Tower by the following given argument:
number of floors (integer and always greater than 0).

Tower block is represented as *


for example, a tower of 3 floors looks like below:

```
[
  '  *  ', 
  ' *** ', 
  '*****'
]
```
and a tower of 6 floors looks like below:
```
[
  '     *     ', 
  '    ***    ', 
  '   *****   ', 
  '  *******  ', 
  ' ********* ', 
  '***********'
]
```

<h3>Solution</h3>

```
def tower_builder(n_floors):
    star_count = 1
    space_count = 1
    tower_output = []
    
    for floor in range(n_floors):
        stars = ('*' * star_count)
        
        space = (' ' * (n_floors - space_count))
        floor_level = space + stars + space
        
        
        print('stars: {}'.format(stars))
        print('floor_level: {}'.format(floor_level))
        
        star_count += 2
        space_count += 1
        tower_output.append(floor_level)
    
    print('tower output: {}'.format(tower_output))
    return tower_output
```
<h2>Count the Smileys</h2>
<h3>Instructions</h3>
Given an array (arr) as an argument complete the function countSmileys that should return the total number of smiling faces.

Rules for a smiling face:
-Each smiley face must contain a valid pair of eyes. Eyes can be marked as : or ;
-A smiley face can have a nose but it does not have to. Valid characters for a nose are - or ~
-Every smiling face must have a smiling mouth that should be marked with either ) or D.
No additional characters are allowed except for those mentioned.

Valid smiley face examples:
:) :D ;-D :~)

Invalid smiley faces:
;( :> :} :] 

<h3>Solution</h3>

```
def count_smileys(arr):
    valid_chars = [':', ';', '-', '~', ')', 'D',]
    count = 0
    
    for face in arr:
        is_eyes = False
        is_smile = False
        valid = True
        
        for symbol in face:
            if symbol not in valid_chars:
                valid = False
            elif symbol == ':' or symbol == ';':
                is_eyes = True
            elif (symbol == ')' or symbol == 'D') and is_eyes and valid:
                is_smile = True
                
            if is_smile and is_eyes:
                count += 1
                
    
    return count
```    
<h2>Sudoku Checker</h2>
<h3>Instructions</h3>
Sudoku is a game played on a 9x9 grid. The goal of the game is to fill all cells of the grid with digits from 1 to 9, so that each column, each row, and each of the nine 3x3 sub-grids (also known as blocks) contain all of the digits from 1 to 9. 
(More info at: http://en.wikipedia.org/wiki/Sudoku)

Write a function validSolution() that accepts a 2D array representing a Sudoku board, and returns true if it is a valid solution, or false otherwise. The cells of the sudoku board may also contain 0's, which will represent empty cells. Boards containing one or more zeroes are considered to be invalid solutions.

The board is always 9 cells by 9 cells, and every cell only contains integers from 0 to 9.

```
test.assert_equals(validSolution([
                         [5, 3, 4, 6, 7, 8, 9, 1, 2], 
                         [6, 7, 2, 1, 9, 5, 3, 4, 8],
                         [1, 9, 8, 3, 4, 2, 5, 6, 7],
                         [8, 5, 9, 7, 6, 1, 4, 2, 3],
                         [4, 2, 6, 8, 5, 3, 7, 9, 1],
                         [7, 1, 3, 9, 2, 4, 8, 5, 6],
                         [9, 6, 1, 5, 3, 7, 2, 8, 4],
                         [2, 8, 7, 4, 1, 9, 6, 3, 5],
                         [3, 4, 5, 2, 8, 6, 1, 7, 9]]), True);
                                
test.assert_equals(validSolution(
                        [[5, 3, 4, 6, 7, 8, 9, 1, 2], 
                         [6, 7, 2, 1, 9, 0, 3, 4, 9],
                         [1, 0, 0, 3, 4, 2, 5, 6, 0],
                         [8, 5, 9, 7, 6, 1, 0, 2, 0],
                         [4, 2, 6, 8, 5, 3, 7, 9, 1],
                         [7, 1, 3, 9, 2, 4, 8, 5, 6],
                         [9, 0, 1, 5, 3, 7, 2, 1, 4],
                         [2, 8, 7, 4, 1, 9, 6, 3, 5],
                         [3, 0, 0, 4, 8, 1, 1, 7, 9]]), False);
                         
```

<h3>Solution</h3>

```
def validSolution(board):
    first_column = []
    second_column = []
    third_column = []
    
    for counter in range(9):
        temp_column = []
        top_square = []
        middle_square = []
        bottom_square = []

        for row in board:
            if len(set(row)) < 9:
                return False
            
            temp_column.append(row[counter])
        
        if len(set(temp_column)) < 9:
            return False
            
        if not first_column:
            first_column = temp_column
        elif not second_column:
            second_column = temp_column
        else:
            third_column = temp_column
            
        if (counter + 1) % 3 == 0:
            top_square = first_column[0:3] + second_column[0:3] + third_column[0:3]
            middle_square = first_column[3:6] + second_column[3:6] + third_column[3:6]
            bottom_square = first_column[6:9] + second_column[6:9] + third_column[6:9]
            
            if len(set(top_square)) < 9 or len(set(middle_square)) < 9 or len(set(bottom_square)) < 9:
                return False
            
            first_column = []
            second_column = []
            third_column = []
            
    return True
```
