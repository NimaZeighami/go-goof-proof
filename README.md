
---

# 📒 Goof-Proof Go 

*A collection of tiny Go notes to help avoid common pitfalls and errors in Go development.*

## 📌 Why This Repo?
While working with Go, it's easy to forget certain gotchas or best practices. This repository is a **personal cheat sheet** to document errors, solutions, and key takeaways to make Go development smoother.

---

## 📖 Table of Contents
#############################
1. [Variables ](#Variables)
2. [Integers](#Integers)
3. [Strings](#Strings)
4. [Constants](#Constants)
#############################

5. 
6. 

---

## Variables 

### ⚠️ One rune literal backslash escape is not legal in a string literal: the single quote escape. It is replaced by a backslash escape for double quotes.

#### ✅var s = "I'm learning Go!"
#### ❌var s = "I\'m learning Go!"
#### ✅var char = '\''
#### ❌var char = '''

### ⚠️ Go enforces simpler naming rules than many languages: it allows Unicode characters (not just English letters) but treats different scripts distinctly, prohibits variable redeclaration, applies the same naming conventions to constants as variables (though UPPER_SNAKE_CASE is conventional for global constants), mandates short names (e.g., i, k) in small scopes for clarity, and requires descriptive names in package blocks—omitting type hints but emphasizing purpose, with brevity signaling scope size and complexity control.

### ⚠️ Some uncommon 64-bit CPU architectures use a 32-bit signed integer for the int type. Go supports three of them: amd64p32, mips64p32, and mips64p32le.

## Integers

### ⚠️ Choosing which integer to use

#### ✅If you are working with a binary file format or network protocol that has an integer of a specific size or sign, use the corresponding integer type.
#### ✅If you are writing a library function that should work with any integer type, take advantage of Go’s generics support and use a generic type parameter to represent any integer type (I talk more about functions and their parameters in
#### ✅In all other cases, just use int.

#### ✅Before Go had generics, developers often created duplicate functions—one using int64 and another using uint64—to handle similar logic for different types. This allowed callers to use type conversions instead of rewriting code. A classic example of this pattern is FormatInt and FormatUint in the strconv package.

### ⚠️ Integer division in Go follows truncation toward zero; see the Go spec’s section on arithmetic operators for the full details.
### ⚠️ be careful not to divide an integer by 0; this causes a panic

##  Floating-points

### ⚠️ A floating-point number cannot represent a decimal value exactly. Do not use them to represent money or any other value that must have an exact decimal representation! Use --- instead (a third party library module !! )
### ⚠️ You can use all the standard mathematical and comparison operators with floats,except %.


### ⚠️ Dividing a nonzero floating-point variable by 0 returns +Inf or -Inf (positive or negative infinity), depending on the sign of the number. Dividing a floating-point variable set to 0 by 0 returns NaN (Not a Number).


### ⚠️ While Go lets you use == and != to compare floats, don’t do it. Because of the inexact nature of floats, two floating-point values might not be equal when you think they should be. Instead, define a maximum allowed variance and see if the difference between two floats is less than that. This value (sometimes called epsilon) depends on your accuracy needs !

### ⚠️ As a language that values clarity of intent and readability, Go doesn’t allow automatic type promotion between variables. You must use a type conversion when variable types do not match. Even different-sized integers and floats must be converted to the same type to interact.
### ⚠️ Go numeric literals are untyped but have type constraints (e.g., no string/int mismatch, no overflow).

## Strings

### ⚠️ strings are compared for equality using ==, difference with !=, or ordering with >, >=, <, or <=. They are concatenated by using the + operator.
### ⚠️ Strings in Go are immutable; you can reassign the value of a string variable, but you cannot change the value of the string that is assigned to it.


### ⚠️ Use runes when dealing with Unicode text manipulation (e.g., counting, reversing, iterating over characters).
### ⚠️ Avoid runes if you're only working with ASCII or simple string operations.

## Constants
### ⚠️ In Go, constants are limited to values that can be determined at compile time, such as numeric literals, booleans, strings, runes, and results of certain built-in functions, and cannot hold complex types like arrays, slices, maps, or functions, with the flexibility of untyped constants, but they cannot be assigned values at runtime.
### ⚠️ In Go, const requires compile-time determinable values, so you cannot use function calls (math.Sqrt(2)), variables (x := 5; const y = x ❌), heap allocations (slices/maps), environment variables (os.Getenv), or dynamic calculations (time.Now().Unix()); But the values returned by the built-in functions complex, real, imag, len, and cap are allowed .

### ⚠️  Constants in Go are a way to give names to literals. There is no way in Go to declare that a variable is immutable.Go doesn’t provide a way to specify that a value calculated at runtime is immutable. (It doesn't have readonly)

### ⚠️ Go constants can be typed (e.g., const x int = 10) or untyped (e.g., const x = 10): untyped constants act like literals with default types for flexible assignments, while typed constants enforce strict type compatibility

### ⚠️ Go allows unused constants because they're compile-time evaluated and have no side effects—unused constants are simply excluded from the compiled binary.



 ---

---
