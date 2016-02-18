# glucca
Glucca is a tiny Javascript ES6 library that generates pseudowords, or words that might not exist but seem like they would. In fact, `glucca` happens to be a pseudoword generated by the algorithm implemented here.

# Usage
    glucca()
It's as simple as that. This returns an array of 2 things: 1) an array used to generate the pseudoword, and 2) the pseudoword itself. To get only the word, do `glucca()[1]`.
# Explanation
There are two stages to this algorithm: generation and translation.
## Generation
An array is generated with the following conditions:
- The array must be of length 4 or 5, no less, no more. However, the algorithm must start with an array of length 4.
- The first item in the array is a random number from 0 to 4.
- For each item after the first item:
  - If the first item is either 0 or 1, the current item is a number from 2 to 6.
  - Otherwise, the current item is randomly 0 or 1.
- If the resulting array ends in a 3, 4, or 6, push randomly 0 or 1 to the array.

## Translation
Each item in the array is translated to its corresponding letter(s) set:

Number|Replacement|Comments
---|---|---
0|`random(a e i o u)`|Vowel.
1|`random(a e i o u)*2`|2 Vowels.
2|`random(d h j k m n s t v w x y z b g p c f l r)`|Consonants.
3|`random(b g p c f)+random(l r)`|"Compatible consonants" - these form realistic consonant combinations. Cannot appear at the end of a pseudoword.
4|`random(st sl sw sh ch th dr tw ph tr wh gh zh)`|More compatible consonants. Cannot appear at the end of a pseudoword.
5|`random(ss tt zz ff ll rr dd)`|Repeated consonants.
6|`random(bb gg cc mm nn pp)`|More repeated consonants. Cannot appear at the end of a pseudoword.
The array of letters joined, any `aa ii uu`'s are made unique (i.e.: `ae`,`io`,`ui`, etc.), and you have yourself a good ol' pseudoword!
# Final Notes
This algorithm was completely independently thought of; I have not seen another generator that uses this algorithm. Its aim is to create reasonably pronounceable pseudowords while being easy to implement.

You may notice that most of the time, word endings are vowels. This is because 2 out of the 7 letter sets during translation are vowels, while 3 out of the 7 letter sets require a vowel to come after. This means that there is a `5/7` chance that a vowel will appear as a pseudoword.

Have fun with `glucca`!
