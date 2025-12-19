---
tags:
  - Book
  - Computer-Science
  - Interpreters
  - Go
  - Golang
  - Programming-Language
  - Programming
  - Software
authors:
  - "[[Thorsten Ball]]"
see:
  - "[[Writing an Interpreter in Go]]"
languages:
original-languages:
translators:
---
[[|< Previous]] | [[|Home]] | [[|Next >]]
# Summary

In this section we write a lexer, which takes source code as input and outputs tokens that represent the source code.

## Notes

Some features that are intentionally being left out:
- Including line number, column number, and filename in a token to produce better error messages
	- p. 15 - `error: expected semicolon token. line 42, column 23, program.monkey`
	- p. 17 - The author recommends we could initialize the lexer with an `io.Reader` and the filename, so that we could track the filename and line numbers in the tokens
		- Prima facie, I would imagine we would want to track newlines that are used as line separators - watching out for escaped ones or ones in strings. What about real newlines vs newlines typed out as characters/literals like `\n`?
	- p. 17 - Ball mentions that to make our lives easier, we are going to use `string` as the type for our source code. Not sure at the time of first reading what this is contrasting with. What else would we use to represent the source code input into the interpreter?
- Floating-point numbers
- Using ASCII instead of Unicode for source code. What would it take to support dealing with runes?
	- p.19 - He mentions that we would need to change, for example, `Lexer.ch` to be a rune rather than a byte, and we would have to change the way that we read next characters, since they would be multiple bytes wide. If we want to approach implementing this differently someday, this might be a helpful resource: https://gobyexample.com/strings-and-runes


Implementation decision from the author:
- Use strings to define token types, rather than int or byte
What are the performance implications of using string? What are the tradeoffs with readability? Could we implement these using something like enums in Go and not lose much readability and maintainability?

p. 19 - We will need to be able to peek ahead in the input
- `position` and `readPosition`

# References

- 

# MOC

- [[Golang]]
- [[Interpreter]]
- [[The Monkey Programming Language]]
- [[Lexical Analysis]] - [[Lexing]] - [[Lexer]]
	- [[Tokenizer]], [[Scanner]]
- [[Abstract Syntax Tree]]
- [[Source Code]] -> [[Token|Tokens]] -> [[Abstract Syntax Tree]]
- [[Data Structures]]
- [[Parser]]
- [[Significant Whitespace]]
- [[Whitespace]]
- [[Production-Ready]]
- [[Python]]
- [[Language]]
- [[Numbers]]
- [[Variable Names]] - [[Identifiers]]
- [[Special Characters]]
- [[Keywords]]
