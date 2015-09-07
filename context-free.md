# Context Free

##  Who is this programming language for?

Computer-aided drawing of images

## What is easy to do in this language? Why is it easy?

Making basic shapes, and to some extend making lines ad paths, are easy. Some
forms of randomness, but not the kind that I would have preferred to use, are
also easy. Modifying these shapes is also very easy, for certain types of
modifications. These things are easy bcause they are supported by the built-in
library and primitive constructs of the language.

## What is hard to do in this language? Why is it hard?

Some forms of randomness, like in expressions instead of choosing rules, are not
only hard but impossible. Other things, like animation, are hard to work with,
but could potentially be worked around. These are both hard because they are not
supported by the built-in library functions; the randomness isn’t even supported
by the language primitives. Both are also easier in version 3.0 of the language.

## How did you learn how to program in this language?

I learned to program in this language by reading some Wiki pages and by
experimentaion. It would have been easier to learn if the documentation had
either a good tutorial or a good reference, but the documentation tried to be
both at once and failed to do a good job of being either.

## What is the underlying _computational model_ for this programming language? 
_We don't yet have a great definition of the term "computational model". 
For now, try to come up with the clearest, most concise explanation of what 
happens when a ContextFree program runs._

Each shape is replaced by one of the rules for generating that shape, or by the
primitive paths. This is repeated recursively until there are only primitive
shapes; shapes too small are dropped to prevent infinite recursion.

This is remarkably similar to how CFGs work, which I only realized while typing
this answer. That probably is where the name comes from.

## What do you think is interesting about the ContextFree program you wrote?

It should have infinite recursion, but the program automatically stops it at 7
iterations. If we were using version 3, it would also produce animations and
interesting randomness.
