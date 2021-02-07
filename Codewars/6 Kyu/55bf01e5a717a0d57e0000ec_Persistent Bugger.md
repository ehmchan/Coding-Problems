## [Persistent Bugger.](https://www.codewars.com/kata/55bf01e5a717a0d57e0000ec)

# Problem
Write a function, persistence, that takes in a positive parameter num and returns its multiplicative persistence, which is the number of times you must multiply the digits in num until you reach a single digit.

For example:

persistence(39) => 3  # Because 3*9 = 27, 2*7 = 14, 1*4=4
                       # and 4 has only one digit.

persistence(999) => 4 # Because 9*9*9 = 729, 7*2*9 = 126,
                       # 1*2*6 = 12, and finally 1*2 = 2.

persistence(4) => 0   # Because 4 is already a one-digit number.
# Solution
```Python
def persistence(n):
    list_num = str(n)
    digits = len(list_num)
    count_reps = 0
    while digits > 1:
        count_reps += 1
        next_num = 1
        for digit in range(digits):
            next_num *= int(list_num[digit])
        list_num = str(next_num)
        digits = len(list_num)
    return count_reps
```

