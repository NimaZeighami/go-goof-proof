
---

# 📒 Goof-Proof Go (or your chosen repo name)

*A collection of tiny Go notes to help avoid common pitfalls and errors in Go development.*

## 📌 Why This Repo?
While working with Go, it's easy to forget certain gotchas or best practices. This repository is a **personal cheat sheet** to document errors, solutions, and key takeaways to make Go development smoother.

---

## 📖 Table of Contents

1. [Variable & Scope ](#variable--scope-issues)
2. [Nil & Pointer Gotchas](#nil--pointer-gotchas)
3. [Concurrency Mistakes](#concurrency-mistakes)
4. [Slices & Maps Quirks](#slices--maps-quirks)
5. [Error Handling Best Practices](#error-handling-best-practices)
6. [Structs & Interfaces Traps](#structs--interfaces-traps)
7. [Performance Tips](#performance-tips)
8. [Other Notes](#other-notes)

---

## 1️⃣ Variable & Scope 

### ⚠️ One rune literal backslash escape is not legal in a string literal: the single quote escape. It is replaced by a backslash escape for double quotes.

#### ✅var s = "I'm learning Go!"
#### ❌var s = "I\'m learning Go!"
#### ✅var char = '\''
#### ❌var char = '''



### ⚠️ Some uncommon 64-bit CPU architectures use a 32-bit signed integer for the int type. Go supports three of them: amd64p32, mips64p32, and mips64p32le.

### ⚠️ Choosing which integer to use

#### ✅If you are working with a binary file format or network protocol that has an integer of a specific size or sign, use the corresponding integer type.
#### ✅If you are writing a library function that should work with any integer type, take advantage of Go’s generics support and use a generic type parameter to represent any integer type (I talk more about functions and their parameters in
#### ✅In all other cases, just use int.

#### ✅Before Go had generics, developers often created duplicate functions—one using int64 and another using uint64—to handle similar logic for different types. This allowed callers to use type conversions instead of rewriting code. A classic example of this pattern is FormatInt and FormatUint in the strconv package.

### ⚠️ Integer division in Go follows truncation toward zero; see the Go spec’s section on arithmetic operators for the full details.
### ⚠️ be careful not to divide an integer by 0; this causes a panic


---

---
