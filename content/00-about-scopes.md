---
title: What is special about Scopes?
type: docs
bookToc: true
weight: 1
---

# What is special about Scopes?

If you don't know how you got here, or are still waiting for a compelling reason to move forward,
below is a rundown of what's different and interesting about the language. At the end I also
state some reasons why you _wouldn't_ want to work with it, depending on your use case.

If you just want to get started learning, it's safe to skip to the next chapter.

## Philosophy and Design

The premise is simple: a language that is easy to use, can be customized to solve any problem, has good iteration times and doesn't sacrifice performance. I wouldn't fault you for thinking that's a snake oil pitch, but a carefully selected set of tradeoffs turns it into a realistic claim.

At its core, it is a systems programming language[^1] like C, C++ or Rust. Unlike most lanaguages in that category, however, it is designed in such a way that types can be very frequently implicitly inferred, giving it a distinct scripting language aesthetic. Generics are also a first class citizen: every function is generic by default (but can be explicitly typed if necessary). While unorthodox, this approach reduces friction both in writing code and replacing it.

## For game developers

In game development, an important concern is to see changes as fast as possible. With the use of the live compiler, we avoid the friction of build systems altogether, and live reloading is trivial to implement for the simple case. Multiple build configurations can also be streamlined by using a different file as the program entry. 

When it comes to distribution, one can either produce a native executable, or bundle the compiler with the application if making use of runtime code compilation. This opens avenues for easy modding, and makes patching the code a non-issue.

Some other useful features in this context include:

- A GLSL-based DSL that targets glsl or SPIR-V from Scopes code. A common pattern of pre processing shaders for project specific needs is obviated by this, since constant embedding and conditional code generation can be done via metaprogramming. Moreover code can be reused between the CPU and GPU portions of the application[^2].
- A vector and matrix library modelled after GLM (and by extension GLSL).
- Can trivially call or be called by C code, due to using the C ABI. Using C libraries involves writing very few lines of code most of the time.

## For language enthusiasts

A common technique when developing a language that targets native code is compiling to C. That remains a good alternative due to the sheer amount of architectures and operating systems supported, but Scopes can be a convenient choice:
- The S-expression based syntax is very easy to generate textually, and if using Scopes for the implementation one can generate lists directly using the API.
- Easy to use solutions for loading and executing code at runtime are provided, eliminating the need to deal with intermediary files in the case of languages that execute from source.
- Strongly typed languages can use a rich and powerful API for type creation, manipulation and reflection.
- Multiple stage based design facilitates building abstractions that offload work from code generation, without compromising the ability to generate a lean build artifact.

Additionally, its metaprogramming features can be used to implement DSLs to power other applications, in a manner similar to how one would approach it in a language like Scheme.

## Drawbacks

Of course, not everything is perfect, and some design decisions lend themselves better to some use cases than others. Keep in mind this section is about the language in its vanilla state - in principle many of the warts can be solved by language extensions and its up to the user to analyze whether the effort is worth it.

The heavy reliance on type inference is a tradeoff between low friction and predictability. It inherits some of the same problems (dynamically typed) scripting languages face, as it's not always clear at a glance what types are at play, and some mistakes can only be caught when functions are actually used, at which point typechecking can occur[^3]. 

[^1]: Meaning it can do lower level operations like addressing memory and emits code without hidden abstractions such as a GC or type boxing.
[^2]: In particular it is useful to be able to execute a shader on the CPU with minimal wrapping for fine grained debugging of program logic.
[^3]: TODO: cite chapter that explains how function instantiation works.
