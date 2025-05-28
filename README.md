# ifnot
esoteric language based around the concept of if/not as a replacement for NAND as a universal operator

if all 16 logical operators can be reduced to sequences of NAND,
then it should also be true that "if" in combination with one other operator
can substitute for NAND, therefore acting as a universal operator
(crazy daydream)(formal proof forthcoming)

# history

After learning that the NAND operator can be used as a logical substitute for all other operators,
I decided to create a language around this idea [nandle](https://github.com/handyc/nandle)
The project did not get very far, mainly because there did not seem to be much application for it.
While chewing on the other 15 logical operators, I had the idea that if NAND and NOR were well
recognized as universal operators, then the other operators must be known not to be universal.
I further reasoned that the addition of one additional operator in combination with the if operator
could be sufficient to act as a logical substitute for NAND.

# but why?

While an entire language made from only combinations of if and not may seem to have limited utility,
it allows for certain fruitful explorations in language and logic that would be difficult to achieve
otherwise.

Examples:
let A = "It is raining."
let B = "I take my umbrella."

If A -> B
"If it is raining, then I take my umbrella."

Consider the truth table for the conditional:

```
A->B
A B C
0 0 1
0 1 1
1 0 0
1 1 1
```

Consider the following human language counterparts to the above table
and evaluate the statement:
"If it is raining, then I take my umbrella."

Situation 1: It's not raining (A is false). I don't take my umbrella.
Analysis: The table returns true, meaning not taking my umbrella follows the rule.
(it was not raining, so it does not matter if I take the umbrella or not)

Situation 2: It's not raining (A is false). I do take my umbrella.
Analysis: The table returns true, meaning taking my umbrella also follows the rule.
(it was not raining, so it does not matter if I take the umbrella or not)

Situation 3: It is raining (A is true). I don't take my umbrella.
Analysis: The table here returns false, meaning not taking my umbrella breaks the rule.
(it is raining, and the rule is that when it's raining I take my umbrella)

Situation 4: It is raining (A is true). I do take my umbrella.
Analysis: The table of course true, meaning taking my umbrella follows the rule.
(it is raining, so I take the umbrella, which is identical to the rule)

Now consider the truth table for NAND, often used as a universal operator:

```
NAND
A B C
0 0 1
0 1 1
1 0 1
1 1 0
```

Here we describe a situation in which the output is true in cases where
it is not true that both A and B are true. In other words, we output true
unless both A and B are both true.

How would this look in terms of human language?
Because the truth table returns different values, we must
revise our human language equivalent with the same A and B as above:

NOT-(it is raining, take my umbrella) 
means
"Either it is raining or I take my umbrella" 

Situation 1: It's not raining (A is false). I don't take my umbrella.
Analysis: The table returns true, meaning not taking my umbrella follows the rule.

Situation 2: It's not raining (A is false). I do take my umbrella.
Analysis: The table returns true, meaning taking my umbrella also follows the rule.

Situation 3: It is raining (A is true). I don't take my umbrella.
Analysis: The table here returns true, meaning not taking my umbrella follows the rule.
This is the situation in which it it raining and I do not take my umbrella,
which may seem foolish in the world but follows the logical rule of
NOT (it is raining, take my umbrella)

Situation 4: It is raining (A is true). I do take my umbrella.
Analysis: The table here returns false, meaning taking my umbrella breaks the rule.
Once again, the truth table does not line up with what we might expect a person to do,
as we cannot satisfy the function when both it is raining and take my umbrella
are true.

# transforming if into NAND

Since we already know that NAND is a universal operator, if we could perhaps
combine the if table with the table of some other operator (e.g. NOT), it seemed
it should be possible to build a function that is logically equivalent to NAND.

...

# idea for combining into one function
thanks to [loudercake](https://github.com/loudercake) for this idea

Presuming the if operator can be combined with the not operator to become
entirely equivalent to the NAND operator, we can perhaps further combine them into a single
operator that governs the entire language.

# a Turing complete language with one operator

the basic idea here is that there is exactly one function for the entire
language and it can be used to create programs that are logically equivalent
to programs in any other Turing complete language.

# OCaml implementation coming soon

...

# Update

After some serious doodling with a real pen on real paper,
it appears to me that the truth table for NAND and the truth
table for A -> NOT-B ("ifnot") are identical,
which means that we may as well just call NAND ifnot instead of attempting
to fuse the conditional and negation operators together some other way.

```
NAND
A B C
0 0 1
0 1 1
1 0 1
1 1 0
```

```
A->B
A B C
0 0 1
0 1 1
1 0 0
1 1 1
```

```
A->NOT-B
A B C
0 0 1
0 1 1
1 0 1
1 1 0
```

# Conclusion

A -> NOT-B is logically equivalent to A NAND B.

Consider once again our human language analyis of A NAND B.
But now that we know that A NAND B is equivalent to A -> NOT-B
we can add an alternative human language interpretation of each
logical situation.

NOT-(it is raining, take my umbrella) means

"Either it is raining or I take my umbrella" 


A -> NOT-B means
"if it is raining then I do NOT take my umbrella"

The truth table and all of the logic involved remain exactly the same,
but only the human language interpretation has changed.

How, then, can we get from here to our original conditional statement of:
"If it is raining, then I take my umbrella."

The answer is absurdly easy. We simply take the opposite of B for the
starting value:

let A = "It is raining."

let B = "I do NOT take my umbrella."


A -> B
"If it is raining, then I do NOT take my umbrella."

A -> NOT-B
"If it is raining, then I take my umbrella."

A NAND B
"Either it is raining or I don't take my umbrella"

For the sake of this convenience, we rename this operator as "ifnot".
Again, it is logically equivalent to NAND in every way,
we are simply calling it "ifnot".

# pseudocode description of ifnot

```
ifnot(string a, string b)
{
return !(A AND B);
}
```

# Nested ifnots

Now let us explore what we can do logically and linguistically by using this operator
as its own input.

let A = "It is raining."

let B = "I do NOT take my umbrella."

A ifnot B = ifnot(A,B)

ifnot(A,B) = "If it is raining, then I take my umbrella."

ifnot(ifnot(A,B), B) = "If (If it is raining, then I take my umbrella), then I take my umbrella"
i.e. if the rule is true, then I take my umbrella (not if the condition it is raining is true)

ifnot(ifnot(A,B), ifnot(B,A)) = "If( if it is raining then I take my umbrella) then (if I take my umbrella then it is raining)."
i.e. if A->B then B->A, also known as biconditional
Biconditional is one of the 16 basic truth tables for operators on binary values of A, B.

We can use other nested ifnots to create the other 14 as well (remember that ifnot itself is NAND):

...


# Example code

```
let A = "cheese"
let B = "rainbow"
let C = ifnot(ifnot(ifnot(ifnot(ifnot(ifnot(ifnot(ifnot(A, B), ifnot(A, B)), ifnot(A, B)), ifnot(A, B)), ifnot(A,B)), ifnot(A,B), ifnot(A, B)), ifnot(A,B))
output C
```
