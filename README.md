
---

# 📒 Goof-Proof Go (or your chosen repo name)

*A collection of tiny Go notes to help avoid common pitfalls and errors in Go development.*

## 📌 Why This Repo?
While working with Go, it's easy to forget certain gotchas or best practices. This repository is a **personal cheat sheet** to document errors, solutions, and key takeaways to make Go development smoother.

---

## 📖 Table of Contents

1. [Variables ](##Variables)
2. [Integers](#Integers)
3. [Concurrency Mistakes](#concurrency-mistakes)
4. [Slices & Maps Quirks](#slices--maps-quirks)
5. [Error Handling Best Practices](#error-handling-best-practices)
6. [Structs & Interfaces Traps](#structs--interfaces-traps)
7. [Performance Tips](#performance-tips)
8. [Other Notes](#other-notes)

---

## Variables 

### ⚠️ One rune literal backslash escape is not legal in a string literal: the single quote escape. It is replaced by a backslash escape for double quotes.

#### ✅var s = "I'm learning Go!"
#### ❌var s = "I\'m learning Go!"
#### ✅var char = '\''
#### ❌var char = '''



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

---

---
