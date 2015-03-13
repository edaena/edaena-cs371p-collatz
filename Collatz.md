# Collatz problem #

---

The Collatz problem was taken from the [Sphere Online Judge](http://www.spoj.pl/problems/PROBTNPO/). It is based on the [collatz conjecture](http://en.wikipedia.org/wiki/Collatz_conjecture) and consists on finding the maximum cycle length in a range of two numbers which are greater than 0 and less than 1000000.



## Algorithm ##

---

The structure of the algorithm is as follows:

_**while**_ user introduces two numbers _i_ and _j_

> _**for**_ each number within the range
> > _**calculate**_ the cycle length
> > _**if**_ cycle length is the greatest seen so far, store the value


> _**print**_ maximum cycle length


The algorithm will terminate when EOF. After the maximum cycle was obtained, the result displays _i_ and _j_ and the maximum cycle length between them.





### Examples ###

For instance, given the numbers 1 and 5 the algorithm will generate the following for each number:

| **Number** | **Collatz conjecture numbers** | **Cycle length** |
|:-----------|:-------------------------------|:-----------------|
| 1 | 1 | 2|
| 2 | 2 1 | 2 |
| **3** | **3 10 5 16 8 4 2 1** | **8** |
| 4 | 4 2 1 | 3 |

As it can be seen on the table, within the range of 1 to 5 the greatest cycle length found is 8 which corresponds to the number 3.

> The answer would be **1 5 8**


### Cycle length calculation ###
The cycle length of a given number is calculated using the [collatz conjecture](http://en.wikipedia.org/wiki/Collatz_conjecture).

#### Example ####
Given the number 5, and applying the conjecture results in the following numbers:
**5, 16, 8, 4, 2, 1** , resulting in a cycle length of **6**. Notice that the number 5 is included in the result.



## Lazy cache ##

---

For this algorithm there are cases when a cycle length can be used more than once to reduce the time required to calculate another cycle length.

Take the range from 1 to 10. Once number 10 is reached following is derived:

10 **5 16 8 4 2 1**

It can be seen that the numbers that follow 10 correspond to the cycle length of 5:

5 16 8 4 2 1


If we store the value of the cycle length of 5, once we reach number 10 we would only need to add 1 to the cycle length of 5 and we would have the cycle length of 10.

> cycle length of 10 = 1 + cycle length of 5

With this idea it is possible to store the cycle length of each number as it is encountered. All this just in case they are useful for calculating the cycle length of a different number.

**Note:** I tried solving the problem by starting computing and storing the cycle lengths of the biggest numbers but this slowed down the whole program instead of speeding it up.


### Storing values ###
In a **lazy cache** values are stored as they are encountered.

When calculating the cycle length of a number:
> _**if**_ you encounter a number whose cycle length was calculated previously
> > _**add**_ that value to the current cycle length and continue with the next number in the range (if any)

> _**else**_ continue calculating the cycle length of the number
> _**store**_ the value of the cycle length that was calculated in the cache




### Array implementation ###
For convenience start filling in a zero to the first array position(in case that it is zero) and store cycle values from position 1 onwards:

The cycle lengths will be stored as:
```
array[0] = 0

array[1] = 1

array[2] = 2

array[3] = 8
```

For this problem an array of 1,000,000 was used. I wanted to try out a cache with more memory but other students mentioned that this didn't speed up the algorithm.