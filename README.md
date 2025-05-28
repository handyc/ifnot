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

...

# idea for combining into one function
thanks to [loudercake](https://github.com/loudercake) for this idea

presuming the if operator can be combined with the not operator to become
entirely equivalent to the NAND operator, we can combine them into a single
operator that governs the entire language

# a Turing complete language with one operator

the basic idea here is that there is exactly one function for the entire
language and it can be used to create programs that are logically equivalent
to programs in any other Turing complete language.

# OCaml implementation coming soon
