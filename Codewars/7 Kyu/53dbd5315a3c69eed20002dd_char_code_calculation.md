## [Char Code Calculation](https://www.codewars.com/kata/57f75cc397d62fc93d000059)

# Problem

Given a string, turn each character into its ASCII character code and join them together to create a number - let's call this number total1:

'ABC' --> 'A' = 65, 'B' = 66, 'C' = 67 --> 656667
Then replace any incidence of the number 7 with the number 1, and call this number 'total2':

total1 = 656667
              ^
total2 = 656661
              ^
Then return the difference between the sum of the digits in total1 and total2:

  (6 + 5 + 6 + 6 + 6 + 7)
- (6 + 5 + 6 + 6 + 6 + 1)
-------------------------
                       6

# Solution
```Python
def calc(x):
    total1 = ""
    total2 = ""
    for char in x:
        code = ord(char)
        total1 += str(code)
    for num in total1:
        if num == "7":
            num = "1"
            total2 += num
        else:
            total2 += num
    num1 = [int(i) for i in total1]
    num2 = [int(i) for i in total2]
    n = sum(num1) - sum(num2)
    return n
```

