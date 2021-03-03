## Usage 101

The rules are defined in a mix of a declarative and a functional programming language.The declarative part is where the natural language is captured. The functional one is where the meaning tree is created.

The implementation is lightweight, and the language is intended for scripting. Once the Asoteric engine is installed into a *nix system, as soon as an `.ast` file is executable and has the respective shebang, Asoteric snippets can be run right away, both interactively and as a production-ready service.

Here's a minimalistic Asoteric snippet:

```
#!/bin/env asoteric
GREETING: (hello | hi) >> ","? >> (world | asoteric) >> "!"? { greering: true }
```

It accepts "hello world", as well as "Hi, Asoteric!", and it transforms these inputs into the `{"greeting":true}` object. Any other input yields the `null` response.

When run from the command line, this snippet would expect queries from the standard input, one per line, and respond with one JSON per line. By using the `-p 3000` parameter, the system would respond with meaning trees to GET request on a specific port. In the interactive way, toggled with `-i`, and enabled by default when run from a terminal that supports it, the script would present more uesr-friendly output with interactive query debugging capabilities. 

In the grammar itself, when defining the `GREETING` term, both the grammar part, `test >> (passed | failed)`, and the meaning part, `{ the_answer: 42 }`, are optional.
