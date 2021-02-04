## [Stop gninnipS My sdroW!](https://www.codewars.com/kata/5264d2b162488dc400000001/train/python)

# Problem
Write a function that takes in a string of one or more words, and returns the same string, but with all five or more letter words reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.

Examples: spinWords( "Hey fellow warriors" ) => returns "Hey wollef sroirraw" spinWords( "This is a test") => returns "This is a test" spinWords( "This is another test" )=> returns "This is rehtona test"

# Solution
```Python
def spin_words(sentence):
    new_sentence = ""
    split_sentence = sentence.split()
    num_words = len(split_sentence)
    for pos_word in range(num_words):
        word = split_sentence[pos_word]
        if len(word) >= 5:
            reversed_word = word[::-1]
            new_sentence += reversed_word
        else:
            new_sentence += word
        if pos_word != num_words-1:
            new_sentence += " "
    return new_sentence
```

