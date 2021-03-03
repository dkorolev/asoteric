## Declarative 101

The `UPPER_CASE` terms, with possible underscores and digits in them, followed by a colon `:`, describe the declarative terms. The declarative terms are what the input textual query is matched against.

Let's focus on single-line input queries now, and assume for now that the input has undergone basic tokenization before being passed to Asoteric logic.

Consider the part of the above example between the colon and the opening curly bracket:

`(hello | hi) >> ","? >> (world | asoteric) >> "!"?`

The basic building blocks for declarative terms are:

* The input query terms. Lowercase words can skip quotes, i.e. `hello` is same as `"hello"`.
* The **OR** operation: `(A | B)` stands for "either A or B".
* The **Chain** operation: `(A >> B)` stands for "A followed by B".
* The **Optional** operation: `A?` stands for "either A or nothing".

For an `UPPERCASE` grammar term to match the input or part of the input, its declarative contents should match the textual content of the input or its part.
