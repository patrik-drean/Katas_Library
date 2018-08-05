# Katas Library
This readme contain varying katas to practice. Listed below each set of instructions is my own initial solution to the probelm.

<h2>Unique Order</h2>
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
