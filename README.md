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

<h2 align="center">Build Tower</h2>
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
<h2 align="center">Count the Smileys</h2>
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
<h2 align="center">Sudoku Checker</h2>
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
<h2 align="center">Zeros to the End</h2>
<h3>Instructions</h3>
Write an algorithm that takes an array and moves all of the zeros to the end, preserving the order of the other elements.

```
move_zeros([false,1,0,1,2,0,1,3,"a"]) # returns[false,1,1,2,1,3,"a",0,0]
```
<h3>Solution</h3>

```
def move_zeros(array):
    return_array = []
    zero_count = 0
    
    for counter in range(len(array)):
        if array[counter] == 0 and array[counter] is not False:
            zero_count += 1
        else:
            return_array.append(array[counter])
    
    for value in range(zero_count):
        return_array.append(0)

    return return_array
```

<h2 align="center">Build a Square</h2>
<h3>Instructions</h3>
I will give you an integer. Give me back a shape that is as long and wide as the integer. The integer will be a whole number between 0 and 50.

Example: Integer = 3; I expect a 3x3 square back just like below as a string.

Solution:

```
+++
+++
+++
```

```
test.assert_equals(generateShape(3), '+++\n+++\n+++')
test.assert_equals(generateShape(8), '++++++++\n++++++++\n++++++++\n++++++++\n++++++++\n++++++++\n++++++++\n++++++++')
```

<h3>Solution</h3>

```
def generateShape(int):
    result_string = ''
    
    for x in range(int):
        result_string += ('+' * int) 
        if (x + 1) != int:
            result_string += '\n'
        
    return result_string
```
<h2 align="center">Scramblies</h2>
<h3>Instructions</h3>

Complete the function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise returns false.

Notes:

Only lower case letters will be used (a-z). No punctuation or digits will be included.
Performance needs to be considered

Examples:

```
scramble('rkqodlw', 'world') ==> True
scramble('cedewaraaossoqqyt', 'codewars') ==> True
scramble('katas', 'steak') ==> False
```

```
Test.assert_equals(scramble('rkqodlw', 'world'),  True)
Test.assert_equals(scramble('cedewaraaossoqqyt', 'codewars'), True)
Test.assert_equals(scramble('katas', 'steak'), False)
Test.assert_equals(scramble('scriptjava', 'javascript'), True)
Test.assert_equals(scramble('scriptingjava', 'javascript'), True)
Test.assert_equals(scramble('patty', 'pat'), True)
Test.assert_equals(scramble('yoda', 'yogurt'), False)
```

<h3>Solution</h3>

```
def scramble(s1, s2):
    for char in s2:
        if char in s1:
            s1 = s1.replace(char, '', 1)
        else:
            return False
            
    return True
```

<h2 align="center">Mumbling</h2>
<h3>Instructions</h3>

This time no story, no theory. The examples below show you how to write function accum:

Examples:

```
accum("abcd")    # "A-Bb-Ccc-Dddd"
accum("RqaEzty") # "R-Qq-Aaa-Eeee-Zzzzz-Tttttt-Yyyyyyy"
accum("cwAt")    # "C-Ww-Aaa-Tttt"
```
The parameter of accum is a string which includes only letters from a..z and A..Z.

<h3>Solution</h3>

```
def accum(s):
    mumbled_string = ""
    counter = 0
    
    for char in s:
        mumbled_string += char.upper()
        mumbled_string += (char.lower() * counter)
            
        if counter != (len(s) - 1):
            mumbled_string += '-'
        
        counter += 1
    
    
    return mumbled_string
```

<h2 align="center">Make the Deadfish Swim</h2>
<h3>Instructions</h3>
Deadfish has 4 commands, each 1 character long:

i increments the value (initially 0)
d decrements the value
s squares the value
o outputs the value into the return array
Invalid characters should be ignored.

```
parse("iiisdoso")  ==>  [8, 64]
```

<h3>Solution</h3>

```
def parse(data):
    value = 0
    result_array = []
    
    for char in data:
        if char == 'i':
            value += 1
        if char == 'd':
            value += -1
        if char == 's':
            value = value**2
            print(value)
        if char == 'o':
            result_array.append(value)
            
    return result_array
```            
<h2 align="center">Index == Value</h2>
<h3>Instructions</h3>

Given a sorted array arr of distinct integers, write a function index_equals_value that returns the lowest index i for which arr[i] == i. Return -1 if there is no such index.

Your algorithm should be very performant.

[input] array of integers

[output] integer

Examples:

```
input: arr = [-8,0,2,5]
output: 2 # since arr[2] == 2

input: arr = [-1,0,3,6]
output: -1 # since no index in arr satisfies arr[i] == i.
```

<h3>Solution</h3>

```
def index_equals_value(arr):
    for index, value in enumerate(arr):
        if index < value:
            return -1
        if index == value:
            return value
```
<h2 align="center">Century from Year</h2>
<h3>Instructions</h3>

The first century spans from the year 1 up to and including the year 100, The second - from the year 101 up to and including the year 200, etc.

Given a year, return the century it is in.

Input , Output Examples ::
centuryFromYear(1705)  returns (18)
centuryFromYear(1900)  returns (19)
centuryFromYear(1601)  returns (17)
centuryFromYear(2000)  returns (20)

```
test.assert_equals(century(1705), 18, 'Testing for year 1705')
test.assert_equals(century(1900), 19, 'Testing for year 1900')
```


<h3>Solution</h3>

```
def century(year):
    century = int(year * .01) 
    if century != (year *.01):
        century += 1
  
    return century
```
