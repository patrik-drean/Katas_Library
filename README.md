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

<h2 align="center">Twice as Old</h2>
<h3>Instructions</h3>
Your function takes two arguments:

current father's age (years)
current age of his son (years)
Сalculate how many years ago the father was twice as old as his son (or in how many years he will be twice as old).

```
Test.assert_equals(twice_as_old(36,7) , 22)
Test.assert_equals(twice_as_old(55,30) , 5)
Test.assert_equals(twice_as_old(42,21) , 0)
```

<h3>Solution</h3>

```
def twice_as_old(dad_years_old, son_years_old):
    doubled_sons_age = son_years_old * 2
    if dad_years_old >= doubled_sons_age:
        return dad_years_old - doubled_sons_age
    else:
        return doubled_sons_age - dad_years_old
```        

<h2 align="center">Count Odd Numbers below Number</h2>
<h3>Instructions</h3>
Given a number n, return the number of positive odd numbers below n, EASY!

```
oddCount(7) //=> 3, i.e [1, 3, 5]
oddCount(15) //=> 7, i.e [1, 3, 5, 7, 9, 11, 13]
```

Expect large Inputs!

<h3>Solution</h3>

```
def odd_count(n):
    if n % 2 == 1:
        return (n - 1) / 2
    else:
        return n / 2
```

<h2 align="center">Multiples of 3 and 5</h2>
<h3>Instructions</h3>
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Finish the solution so that it returns the sum of all the multiples of 3 or 5 below the number passed in.

Note: If the number is a multiple of both 3 and 5, only count it once.


```
test.assert_equals(solution(10), 23)
```

<h3>Solution</h3>

```
def solution(number):
    total_sum = 0
    num = number - 1
    for x in range(number):
        if num % 3 == 0 or num % 5 == 0:
            total_sum += num
        num -= 1
            
    return total_sum
```

<h2 align="center">Even or Odd</h2>
<h3>Instructions</h3>
Create a function that takes an integer as an argument and returns "Even" for even numbers or "Odd" for odd numbers.

```
test.expect(even_or_odd(2) == "Even")
test.expect(even_or_odd(0) == "Even")
test.expect(even_or_odd(7) == "Odd")
test.expect(even_or_odd(1) == "Odd")
```

<h3>Solution</h3>

```
def even_or_odd(number):
    if number % 2 == 0:
        return 'Even'
    else:
        return 'Odd'
```

<h2 align="center">Shortest Word</h2>
<h3>Instructions</h3>
Simple, given a string of words, return the length of the shortest word(s).

String will never be empty and you do not need to account for different data types.

```
test.assert_equals(find_short("bitcoin take over the world maybe who knows perhaps"), 3)
test.assert_equals(find_short("turns out random test cases are easier than writing out basic ones"), 3)
```

<h3>Solution</h3>

```
def find_short(s):
    word_list = s.split()
    print(word_list)
    l = -1
    
    for word in word_list:
        if len(word) < l or l == -1:
            l = len(word)
        
    return l # l: shortest word length
```

<h2 align="center">Stop gninnipS My sdroW!</h2>
<h3>Instructions</h3>
Write a function that takes in a string of one or more words, and returns the same string, but with all five or more letter words reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.

```
test.assert_equals(spin_words("Welcome"), "emocleW")
```

<h3>Solution</h3>

```
def spin_words(sentence):
    word_list = sentence.split()
    finalized_words = []
    
    for word in word_list:
        if len(word) >= 5:
            updated_word = word[::-1]
            finalized_words.append(updated_word)
        else:
            finalized_words.append(word)
            
    
    return ' '.join(finalized_words)
```

<h2 align="center">CamelCase</h2>
<h3>Instructions</h3>
Write simple .camelCase method (camel_case function in PHP, CamelCase in C# or camelCase in Java) for strings. All words must have their first letter capitalized without spaces.

```
camelcase("hello case") => HelloCase
camelcase("camel case word") => CamelCaseWord
```

<h3>Solution</h3>

```
def camel_case(string):
    word_list = string.split()
    camel_case_string = ""
    
    for word in word_list:
        camel_case_string += word.capitalize()
    
    return camel_case_string
```

<h2 align="center">Sum Consecutives</h2>
<h3>Instructions</h3>
You are given a list/array which contains only integers (positive and negative). Your job is to sum only the numbers that are the same and consecutive. The result should be one list.

Extra credit if you solve it in one line. You can asume there is never an empty list/array and there will always be an integer.

Same meaning: 1 == 1

[1,4,4,4,0,4,3,3,1] # should return [1,12,0,4,6,1]

<h3>Solution</h3>

```
def sum_consecutives(s):
    final_list = []
    last_digit = s[0]
    count = 0
    
    for index, digit in enumerate(s):
        if digit == last_digit:
            count += 1
        else:
            final_list.append(count * last_digit)
            count = 1
                     
        if index == len(s) - 1:            
            if digit == last_digit:
                final_list.append(count * digit)
            else:
                final_list.append(digit)

            
        last_digit = digit
        
    return final_list

```

<h2 align="center">You're a square</h2>
<h3>Instructions</h3>
A square of squares
You like building blocks. You especially like building blocks that are squares. And what you even like more, is to arrange them into a square of square building blocks!

However, sometimes, you can't arrange them into a square. Instead, you end up with an ordinary rectangle! Those blasted things! If you just had a way to know, whether you're currently working in vain… Wait! That's it! You just have to check if your number of building blocks is a perfect square.

Task
Given an integral number, determine if it's a square number:

In mathematics, a square number or perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself.

The tests will always use some integral number, so don't worry about that in dynamic typed languages.

```
is_square (-1) # => false
is_square   0 # => true
is_square   3 # => false
is_square   4 # => true
is_square  25 # => true
is_square  26 # => false
```

<h3>Solution</h3>

```
import math

def is_square(n):  
    
    if n < 0:
        return False

    return  (int(math.sqrt(n)) * int(math.sqrt(n))) == n

```

<h2 align="center">Duck, Duck, Goose (C#)</h2>
<h3>Instructions</h3>
The objective of 'Duck, duck, goose' is to walk in a circle, tapping on each player's head until one is finally chosen. 

Task: Given an array of Player objects and an index (1-based), return the name of the chosen Player. 

```
using NUnit.Framework;
using System;
using System.Linq;

namespace Solution 
{
   [TestFixture]
  public class PlayerTests
  {
    [TestCase(1,  "a")]
    [TestCase(3,  "c")]
    [TestCase(11,  "a")]
    [TestCase(14,  "d")]

    public void DuckDuckGooseTests(int goose, string expectedName)
    {
      var exampleNames = new string[] {"a", "b", "c", "d", "c", "e", "f", "g", "h", "z"};
      var players = exampleNames.Select(x=>new Player(x)).ToArray();
      string userAns = Kata.DuckDuckGoose(players,goose);
      Assert.AreEqual(expectedName, userAns);
    }
  }
  
  
}
```

<h3>Solution</h3>

```
using System;

public class Kata
{
  public static string DuckDuckGoose(Player[] players, int goose)
  {   
    int goose_pos = goose - 1;
    
    if (goose_pos >= players.Length)
    {
      goose_pos = goose_pos % players.Length;
    }
    
    return players[goose_pos].Name;
  }
}
public class Player 
{
  public string Name {get;set;}
  
  public Player (string name) 
  {
	  this.Name = name;
  }
}
```

<h2 align="center">High Number (C#)</h2>
<h3>Instructions</h3>
Given 3 integers, write the code to return the largest product of them. Remember to consider negative integers in writing the solution.  

```
using System;
using NUnit.Framework;

[TestFixture]
public static class AccumulTests 
{

    private static void testing(int actual, int expected) 
    {
        Assert.AreEqual(expected, actual);
    }

[Test]
    public static void test1() 
    {
      int[] numbers = new int[]{2,1,0};
      testing(Accumul.Accum(numbers), 2);
        
    }
}
```

<h3>Solution</h3>

```
using System;

public class Accumul 
{
	public static int Accum(int[] numbers) 
  {
    int high_num = numbers[0];
    
    foreach (int num in numbers) 
    {
       if (num > high_num) 
       {
         high_num = num;
       }
    }
  
    return high_num;
  }
}
```

<h2 align="center">Return Negative (C#)</h2>
<h3>Instructions</h3>
In this simple assignment you are given a number and have to make it negative. But maybe the number is already negative?

```
using NUnit.Framework;

[TestFixture]
public class Tests
{
  [Test]
  public void PositiveToNegative()
  {
    Assert.AreEqual(-42, Kata.MakeNegative(42));
  }
    [Test]
  public void NegativeToNegative()
  {
    Assert.AreEqual(-42, Kata.MakeNegative(-42));
  }
}
```

<h3>Solution</h3>

```
using System;

public static class Kata
{
  public static int MakeNegative(int number)
  {
    if (number > 0)
    {
      return number - (number * 2);
    }
    else if (number < 0 )
    {
      return number;
    }
    else
    {
      return 0;
    }
    
  }
}
```


<h2 align="center">Sum of Positive (C#)</h2>
<h3>Instructions</h3>
You get an array of numbers, return the sum of all of the positives ones.

Example [1,-4,7,12] => 1 + 7 + 12 = 20

Note: if there is nothing to sum, the sum is default to 0.

```
using NUnit.Framework;
using System;

[TestFixture]
public class Tests
{
  [Test]
  [TestCase(new int[]{1, 2, 3, 4, 5}, ExpectedResult=15)]
  [TestCase(new int[]{1, -2, 3, 4, 5}, ExpectedResult=13)]
  [TestCase(new int[]{-1, 2, 3, 4, -5}, ExpectedResult=9)]
  [TestCase(new int[]{}, ExpectedResult=0)]
  [TestCase(new int[]{-1, -2, -3, -4, -5}, ExpectedResult=0)]
  public static int ExampleTest(int[] arr)
  {
    return Kata.PositiveSum(arr);
  }
}
```

<h3>Solution</h3>

```
using System;

public class Kata
{
  public static int PositiveSum(int[] arr)
  {
    int sum = 0;
    
    foreach (int num in arr) 
    {
      if (num > 0) 
      {
        sum += num;
      }
    }
    
    return sum;
  }
}

```

<h2 align="center">Find the odd counted int (C#)</h2>
<h3>Instructions</h3>
Given an array, find the int that appears an odd number of times.

There will always be only one integer that appears an odd number of times.

```
namespace Solution {
  using NUnit.Framework;
  using System;

  [TestFixture]
  public class SolutionTest
  {
    [Test]
    public void Tests()
    {
      Assert.AreEqual(5 , Kata.find_it ( new[] { 20,1,-1,2,-2,3,3,5,5,1,2,4,20,4,-1,-2,5 }));
    }
  }
}
```

<h3>Solution</h3>

```
using System.Collections.Generic;
using System.Linq;
using System;

namespace Solution
{
  class Kata
    {
    public static int find_it(int[] seq) 
      {
        var values = new List<List<int>>();

        foreach (int num in seq) 
        {
          bool numberAddedAlready = false;
          
          foreach (var listOfSameNumber in values)
          {
            if (num == listOfSameNumber[0]) 
            {
              listOfSameNumber.Add(num);
              numberAddedAlready = true;
            }
          }
          
          if (! numberAddedAlready )
          {
            values.Add(new List<int> {num});
          }
        }
        
        return (values.Where(x => x.Count() % 2 == 1)).ToList()[0][0];
      }
       
    }
}
```

<h2 align="center">Playing with Digits (C#)</h2>
<h3>Instructions</h3>
Some numbers have funny properties. For example:

89 --> 8¹ + 9² = 89 * 1

695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2

46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51

Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p we want to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n. In other words:

Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k

If it is the case we will return k, if not return -1.

Note: n, p will always be given as strictly positive integers.

```
using System;
using System.Collections.Generic;
using NUnit.Framework;

[TestFixture]
public class DigPowTests {

[Test]
  public void Test1() {
    Assert.AreEqual(1, DigPow.digPow(89, 1));
  }
[Test]
  public void Test2() {
    Assert.AreEqual(-1, DigPow.digPow(92, 1));
  }
[Test]
  public void Test3() {
    Assert.AreEqual(51, DigPow.digPow(46288, 3));
  }
}

```

<h3>Solution</h3>

```
using System;
using System.Collections.Generic;

public class DigPow {
	public static long digPow(int n, int p) {
    string nAsString = n.ToString();
    int resulting_factor = -1;
    int sum = 0;
    
    foreach (char charDigit in nAsString) 
    {
       int digit = int.Parse(charDigit.ToString());
       sum += (int) Math.Pow(digit, p );
       p++;
       Console.WriteLine(sum);
    }
    
    if (sum % n == 0)
    {
      resulting_factor = sum / n;
    }

		return resulting_factor;
	}
}
```

<h2 align="center">Tribonacci Sequence</h2>
<h3>Instructions</h3>
Well met with Fibonacci bigger brother, AKA Tribonacci.

As the name may already reveal, it works basically like a Fibonacci, but summing the last 3 (instead of 2) numbers of the sequence to generate the next. And, worse part of it, regrettably I won't get to hear non-native Italian speakers trying to pronounce it :(

So, if we are to start our Tribonacci sequence with [1, 1, 1] as a starting input (AKA signature), we have this sequence:

[1, 1 ,1, 3, 5, 9, 17, 31, ...]


```
using NUnit.Framework;

[TestFixture]
public class XbonacciTest
{
  private Xbonacci variabonacci;
  
  [SetUp]
  public void SetUp() 
  {
    variabonacci = new Xbonacci();
  }

  [TearDown]
  public void TearDown()
  {
    variabonacci = null;
  }

  [Test]
  public void Tests()
  {
    Assert.AreEqual(new double []{1,1,1,3,5,9,17,31,57,105}, variabonacci.Tribonacci(new double []{1,1,1},10));
    Assert.AreEqual(new double []{0,0,1,1,2,4,7,13,24,44}, variabonacci.Tribonacci(new double []{0,0,1},10));
    Assert.AreEqual(new double []{0,1,1,2,4,7,13,24,44,81}, variabonacci.Tribonacci(new double []{0,1,1},10));
  }
}
```

<h3>Solution</h3>

```
using System;
using System.Collections.Generic;

public class Xbonacci
{
  public double[] Tribonacci(double[] signature, int n)
  {
    double first_value = signature[0];
    double second_value = signature[1];
    double third_value = signature[2];
    
    double[] final_sequence = new double[n];
    final_sequence[0] = first_value;
    final_sequence[1] = second_value;
    final_sequence[2] = third_value;
    
    for (int x = 3; x < n ; x++) 
    {
      double summed_value = first_value + second_value + third_value;
      final_sequence[x] = summed_value;
      
      first_value = second_value;
      second_value = third_value;
      third_value = summed_value;
    }
    
    return final_sequence;
    
  }
}
```

<h2 align="center">Reverse Words in a Phrase (C#)</h2>
<h3>Instructions</h3>
Complete the function that accepts a string parameter, and reverses each word in the string. All spaces in the string should be retained.

```
namespace Solution
{
  using NUnit.Framework;
  
  [TestFixture]
  public class Tests
  {
    [Test]
    public void Example()
    {
      Assert.AreEqual("sihT si na !elpmaxe", Kata.ReverseWords("This is an example!"));
    }
  }
}
```

<h3>Solution</h3>

```
using System;
using System.Collections.Generic;

public static class Kata
{
  public static string ReverseWords(string str)
  {
    var splitWords = str.Split(" ");
    var reversedSplitWords = new List<string>();
    
    foreach (string word in splitWords)
    {
      string reversedString = "";
      
      for (int x = word.Length - 1; x >= 0 ; x--) 
      {
        reversedString += word[x].ToString();
      }
      
      reversedSplitWords.Add(reversedString);
    }
    
    return string.Join(" ", reversedSplitWords);
  }
}
```

<h2 align="center">Find the next perfect square (C#)</h2>
<h3>Instructions</h3>
You might know some pretty large perfect squares. But what about the NEXT one?

Complete the findNextSquare method that finds the next integral perfect square after the one passed as a parameter. Recall that an integral perfect square is an integer n such that sqrt(n) is also an integer.

If the parameter is itself not a perfect square, than -1 should be returned. You may assume the parameter is positive.

```
using NUnit.Framework;
using System;

[TestFixture]
public class Tests
{
  [Test]
  [TestCase(155, ExpectedResult=-1)]
  [TestCase(121, ExpectedResult=144)]
  [TestCase(625, ExpectedResult=676)]
  [TestCase(319225, ExpectedResult=320356)]
  [TestCase(15241383936, ExpectedResult=15241630849)]
  public static long FixedTest(long num)
  {
    return Kata.FindNextSquare(num);
  }
}
```

<h3>Solution</h3>

```
using System;

public class Kata
{
  public static long FindNextSquare(long num)
  {
    double squareRootedValue = Math.Sqrt(num);
    if (squareRootedValue % 1 == 0) 
    {
      return (long) Math.Pow((squareRootedValue + 1), 2);
    }
    else
    {
      return -1;
    }
  }
}
```
