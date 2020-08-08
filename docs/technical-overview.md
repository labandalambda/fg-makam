

# fg.makam

This is the first file we worked on and the best starting point for the project. Here we define all the necessary types and constructors to define Featherweight Go's Abstract Syntax Tree.

We will be defining the language in terms of types and constructors. So an expression is represented as a type, a expression nodes can be constructed using different constructs, such as struct literals and method calls.

We will be basing the AST on the calculus presented on Figure 9, FG syntax, from [paper].

We will set representations which we'll use in the code. Field names and field methods will be represented as Makam strings. An FG type, whether it is ts (struct type) or ti (interface type), or just arbitrary t, will be represented also as a string. This seems confusing but will eventually become much clearer. Hang in there reader! Just a few more paragraphs before everything becomes clearer.

```
% Fig 9
% -----
% FG syntax

% field = string.
% method = string.
% variable ???
% ts, ti, t = string.
```
