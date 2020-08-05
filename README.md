# fg-makam
Featherweight Go implementation in Makam[[1]](#1).

This implementation is only educational and was used to learn Makam in the process.

Featherweight Go is a minimalist version of Go defined by Griesemer et al. in their paper.[[2]](#2)

Makam is a metalanguage that eases implementation of languages, aimed at allowing rapid prototyping[[3]](#3) and experimentation with new programming language research ideas.

## Idea
Implement the "Featherweight Go" calculus presented in section 3 of Griesemer et al.[[2]](#2)

The implementation was made as simple as possible. For that purpose, the code is very close to the actual mathematical calculus presented in the paper.[[1]](#1)

The differences between the code and the calculus arise only when those changes simplify the implementation details.

## Goals

 * Learn Makam
 * Show how easy it is to prototype a programming language with Makam
 * Have a better understanding of "Featherweight Go"[[1]](#1)
 * Compare this implementation to [the paper's accompanying implementation](https://github.com/rhu1/fgg)

## Future work

 * Implement FGG (Featherweight Generic Go)
 * Implement monomorphization (an ambitious goal)
 * Improve parsing

# References
<a id="1">[1]</a>
[Makam:](https://github.com/astampoulis/makam) The Makam metalanguage -- a tool for rapid language prototyping

<a id="2">[2]</a>
[Featherweight Go](https://arxiv.org/pdf/2005.11710.pdf) Griesemer et al.

<a id="3">[3]</a>
[How to make your papers run: Executable formal semantics for your language](https://www.tweag.io/blog/2019-11-28-PCF-makam-spec/)
