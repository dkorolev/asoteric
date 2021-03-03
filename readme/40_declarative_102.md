## Declarative 102

There exists a special term, `EMPTY`, which only matches an empty [part of] the input.

The rules for accepting the user input are not the "yes / no" ones, but rather an iterator, which can yield zero, one, or more possible matches. The intuitive way to think about it is that more than one option in the OR clause can match [part of] the input, and all OR options will be considered.

The options in the OR clause are considered left to right. A simple way to illustrate it is by expanding the meaning of the "Optional" clause. A single question mark, such as `TERM: foo?` is equivalent to `TERM: foo | EMPTY`.

By analogy with regular expressions, a single question mark is the "greedy optional", and a question mark repeated twice is the "forgiving" one. In other words, `TERM: foo??` is equivalent to `TERM: EMPTY | foo`.

With the rules consisting of just one optional `foo`, the result of applying Asoteric to an input query of a single word "foo" is indistinguishable whether the greedy or the forgiving version of optionality is used.

Where the distinction comes into play is when multiple ways to parse the input are possible. In this case, greediness, as well as the order of "OR" clauses, define the order in which different matchings are tried. In the case of regular expressions, just the first possible match will be returned. In the case of Asoteric, the engine iterates over them, and the functional part of the logic comes into play here.

Example:

```
FOO_BAR: foo >> bar?
BAR_BAZ: bar? >> baz
FOO_BAR_BAZ: FOO_BAR >> BAR_BAZ
```

When matching the "foo bar baz" input against the `FOO_BAR_BAZ` term, two possible ways to parse the input are possible, with "bar" being part of the `FOO_BAR` term or a part of the `BAR_BAZ` one.

With a single question mark in the first line, "bar" would first be parsed to be part of `FOO_BAR`, and then as part of `BAR_BAZ`. With `FOO_BAR: foo >> bar??`, the forgiving optional, "bar" would first be caught by the `BAR_BAZ` term, and only then by the `FOO_BAR` term.

Obviously, with no functional part to complement the declarative one above, the end user would not see the difference. But this order matters, both to the functional part of the rules, and to the logic outside Asoteric that invokes the Asoteric engine as part of its business logic and iterates over the matches in the order they are provided.

Also, in the above example, the chaining operation used is `>>`. It corresponds to the natural left-to-right parsing, with path prioritization working identially with how the regular expression would accept the above input. Other chaining operators, `<<` and more, can be used to fine-tune the parsing.
