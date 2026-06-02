# Capstone GO Project

There are **two different “speeds” when comparing programming languages** :

1. **Runtime speed** – how fast the compiled program _runs_
2. **Compile-time speed** – how fast the compiler _finishes compiling your code_

> Go programs don't run quite as fast as its compiled Rust, Zig, and C counterparts.
> 
> But, it **compiles much faster** than they do.

So:

- Compared to **interpreted languages** (Python, JS, Ruby), Go programs usually **run faster** →
- Compared to **other compiled languages** (C, Rust, Zig), Go **compiles faster** (even if it _runs_ a bit slower) → `faster`

**In one folder (package), you can have only ONE `func main()`**.

**Go runs programs, not files.**

A program = one folder (package).

To declare a variable and assign the value with the type directly in go we use “:=” operator, not valid for “const”.

fmt.Printf("My weight on the surface of %v is %v lbs.\n", "Earth", 149.0)

msg = fmt.Sprintf(”Hi, my name is %s and I am %.2f years old”, name, age)

constants in go can be computed at compile time.

similar to what a character is, we have unicode, and in go there is a different data type to deal with unicodes that is called rune, it isa 32 bit placeholder.

### If statement in Go:

```go
a := 5, b := 10
if a>b {
	fmt.Println(a, "is bigger than", b)
} else { // in golang, else mustbe on the same line that if ends, since ; in inserted every line break
	fmt.Println("%v is not bigger than %v", a, b)
	}
```

### Switch Statements in Go:

### Loops in Go:

1. For Loop

2. While Loop

### Functions in Go:

```go
package main
//  a function must have the return types it is taking as inputs and show the return type as well in the function signature
func concatenate(s1 string, s2 string) string {
	return s1 + s2
}
//functions in go can have multiple return values, just specify both reurn value types in {} 
```

Since go does not allow you to have unused variables, we use “_” when we want to ignore one variable that a function might be giving as output among many.

Guard Clauses leverage the ability to `return` early from a function (or `continue` through a loop) to make nested conditionals one-dimensional. Instead of using if/else chains, we just return early from the function at the end of each conditional block.