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

Bit masking toy example that we talked about to illustrate what the strategy is in the Go standard library while exploring the question "what would it really take to implement unicode support in Monkey?" (spoiler: a lot)

[isLower from unicode package in go src](https://cs.opensource.google/go/go/+/refs/tags/go1.25.5:src/unicode/letter.go;drc=b8e533a7cdc60d84a0c52bfaf3dcb5bf148ac3a8;l=193)

```
uppercase = 00000010
lowercase = 00000001

lettermask = 00000011
some_letter = 11010010

some_letter&lettermask == uppercase // true
```

p. 20 - What are good practices around structuring tests for situations like this, where we are building out a lexer incrementally? At first I wanted to object to the approach taken in the book, but I'm more comfortable with it on reflection, since the lexer should be able to read any valid input. It might be desirable to have smaller tests that check particular sequences in isolation, since that would make the tests more readable, though. Worth looking into how people approach this in production interpreters.

pp. 21-2 - What operators might be useful in a programming language? Are there any that I wish that I had? Perhaps in some DSLs, it would be more desirable than elsewhere to have quirky ones for mathematical operations and such. I wonder also how people approach the problem of operator overloading, where the user of that language can define their own operators. How do you go about doing this at runtime? Do different language families have different approaches to this? Will it make a difference whether the language is compiled or interpreted for this question in particular?

p. 23 - peekChar is a delightful function. Under what circumstances should operators be two, three, or more characters long? (Take, for example the triple-equals operator in Javascript). What are the limits that languages do in fact impose, and what reasons are there for exceeding them? What tradeoffs do those exceptional cases introduce to the language design?

p. 25 - The REPL uses `bufio` for reading in the input from the terminal. Under what circumstances is it better to use `bufio` rather than `io`?

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
- [[Operators]]
- [[JavaScript]]
- [[Parser]]
- [[Read-Ahead]]
- [[REPL]]
