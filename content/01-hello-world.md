---
title: Hello, world!
type: docs
bookToc: true
weight: 1
---
# Hello, world!

As is tradition, this is our first Scopes program:

    print "Hello, world!"
    
Save it as `hello-world.sc` and run it like so:

    scopes hello-world.sc
    
Notice we didn't produce an executable, but ran it using the compiler, similar to what one would do in a scripting language.
Also, there's no main function. So how does it work?

For now, all you need to know is that the module you launch as your program is the equivalent to your main function. The compiler parses it, compiles then wraps it from its own main, on the fly. Later on we'll explore in depth what's really happening behind the scenes, and other ways to execute code. And yes, you **can** make a traditional executable.
    
You can also use the REPL. Just run scopes without arguments:

     ❯ scopes
      \\\
       \\\   Scopes 0.17 (Sep  6 2020, 17:53:07)
     ///\\\  http://scopes.rocks
    ///  \\\
    $0 ► print "hello world"
    hello world
    $0 ► 
    
I won't talk much about the REPL on this tutorial, because it's very often the same as just running from a file, and the [official docs](https://scopes.readthedocs.io/en/latest/tutorial/#interactive-console)
already cover it pretty well. But it's very useful to quickly experiment with some snippet or poke at a feature of the language. 
It's also just as powerful! You can even use C libraries from it, because it's the same runtime - just live compiling whatever you type in.

In general you'll want to use the REPL for more quick prototyping, since it gets less convenient the more you type.
