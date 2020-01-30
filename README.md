# Rewriting Playground

Just some experiments using [Enki](https://github.com/ReedOei/Enki), a programming language I wrote, to implement some concepts from rewriting logic.

At the moment it's a simple rewriting interpreter that let's you define rewrite rules and then evaluates a given term using those rules.

For example, the following program contains rewrite rules for defining addition and multiplication on natural numbers represented as `0`, `s(0)`, and so forth.
It calculates `5 * 6`.
To run it, use `enki run rewriting.enki`

```
nat rules are
    cons (rl (bifunc "+" (constant 0) (variable "M")) => (variable "M")) (
    cons (rl (bifunc "+" (func "s" (variable "N")) (variable "M")) => (func "s" (bifunc "+" (variable "N") (variable "M")))) (
    cons (rl (bifunc "*" (constant 0) (variable "M")) => (constant 0)) (
    cons (rl (bifunc "*" (func "s" (variable "N")) (variable "M")) => (bifunc "+" (variable "M") (bifunc "*" (variable "N") (variable "M")))) empty))).

as succ nat N is
    when N = 0 then constant 0.
    when N > 0 then func "s" (as succ nat (N - 1)).
    otherwise then false, variable "NONSENSE".

A = as succ nat 3,
B = as succ nat 6,
display format term evaluate (bifunc "*" A B) using nat rules.
```

