# Rewriting Playground

Some experiments using [Enki](https://github.com/ReedOei/Enki), a programming language I wrote, to implement some concepts from rewriting logic.

At the moment it's a simple rewriting interpreter that let's you define rewrite rules and then evaluates a given term using those rules.

For example, the following program contains rewrite rules for defining addition and multiplication on natural numbers represented as `0`, `s(0)`, and so forth.
It calculates `2 * 10`.
To run it, use `enki run rewriting.enki`

```
nat rules are
    cons (parse rule "+(0,M)=>M") (
    cons (parse rule "+(s(N),M)=>s(+(N,M))") (
    cons (parse rule "*(0,M)=>0") (
    cons (parse rule "*(s(N),M)=>+(M,*(N,M))") (
    cons (parse rule "if(0,A,B)=>A") (
    cons (parse rule "if(1,A,B)=>B") empty))))).

as succ nat N is
    when N = 0 then constant 0;
    when N > 0 then func "s" (as succ nat (N - 1)).

A = as succ nat 2,
B = as succ nat 10,
BaseTerm = parse term "*(A,B)",
Term = substitute in BaseTerm using (cons ("A" |-> A) (cons ("B" |-> B) empty)),
display format term evaluate Term using nat rules.
```

