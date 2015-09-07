# Language
_What is the name of the language? Link the name to its webpage 
(if appropriate)._

The language is called [ACSL](http://frama-c.com/acsl.html), but the tools to
work with it are collectively [Frama-C](http://frama-c.com/what_is.html) and a
variety of [plugins](http://frama-c.com/plugins.html).

# Domain
_Describe the language's domain in five words._

Formal specifications for C code


# Computational model
_What is the underlying computational model of this language? To answer this 
question, provide a high-level description (no more than 100 words) of the 
computation that occurs when someone executes a program in this language._

ACSL is not exactly an executable language, _per se_, and what happens depends
very much on the plugins used. It is a specification language, which can be used
to add assert statements, prove functions correct, prove loops terminate, or
other things. This is done by a Frama-C plugin or plugins reading the
declarative specifications to figure out what it needs to do (e.g., what
assertions to add, what test cases to prove, etc.), and then attempting to do
it (e.g., output new C code with additional assert statements, give cases to a
theorem prover, etc.).


# DSL-ness
_Fowler writes about a spectrum of languages, from general-purpose languages to 
"purely" domain-specific. Where does the DSL you chose fall on this spectrum, 
and why?_ 

ACSL is almost purely domain-specific, but can encode arbitrary mathematical
specifications and therefore Turing-complete computations. I can’t see why
anybody would use ACSL as a general-purpose language, but it is theoretically
possible. In this case, I would classify ACSL as slightly more domain-specific
than the XSLT example that Fowler mentions. It can theoretically do anything,
but it is much more focussed on formal specification of other code than XSLT is
on transforming XSL, and is always used that way in practice (when it is used).
This is especially apparent because (I believe) Frama-C will not actually run
arbitrary computations encoded in ACSL, making it in practice Turing-incomplete
even if theoretically it could be Turing-complete.

# Internal or external?
_Is the language implemented as an internal or external DSL? 
Justify your answer._

This is an external DSL. Even though it is usually embedded in other C files, it
is put into the comments of the file and ignored by the compiler. The ACSL
annotations form a language by themselves which depends on C, but is not itself
C. This is similar to how Fowler calls regular expressions an external DSL on
page 32, but even more external because they are in the host language's comments
instead of strings.

# Host language
_What language(s) was (were) used to implement the DSL?_

The C language is closely tied to ACSL, so I would like to be especially clear
here. ACSL (the language) is a language that is typically but not always located
in specific annotations of C source code. It is also possible to write ACSL
outside of any C source files; this is part of what makes it an external DSL. As
ACSL is a language, it could theoretically be implemented by any tool; there is
nothing stopping somebody from taking
[the specification](http://frama-c.com/download/acsl.pdf) and implementing it in
Haskell, D, or Python.

The main tools which are developed to work with ACSL are Frama-C and various
plugins. I have not checked any of the plugins, but it appears that the bulk of
Frama-C was written in OCaml, although I would be shocked if there was no C in
the imlementation also.

Therefore, I would suggest that from the developer’s point of view, the host
language is primarily OCaml with some C. However, from the point of view of the
user of the language, it would make more sense to say that the host language is
almost entirely C. This is similar to how the DSL for makefiles is implemented
by (various versions of) make, most but not all of which were written in C, but
it would still make sense to some extend to say that the language was hosted by
the Bourne shell scripting language.


# Benefits
_Identify one potential benefit of the DSL: how is a programmer's life or a 
company's bottom line made easier by the existence of this language?_

Proper use of ACSL and Frama-C can help ensure that programs perform as the
programmers intended, or help find bugs. Even using ACSL without Frama-C (or,
for that matter, Frama-C without ACSL) can help spot some kinds of bugs and help
programmers think of edge cases.

# Drawbacks
_Identify one potential drawback of the DSL: what does a programmer or company 
lose by using this DSL instead of a general-purpose language?_

Theoretically, if one were to write all the specifications in a general
laguage, one could write specifications which ACSL does not currently support,
or perhaps extend it to work beyond C in some cases more easily.

However, comparing ACSL to a general language is not really the correct
comparison: the alternative to using ACSL is in most cases not using any sort of
formal specification language; this is the path taken by the vast majority of
projects. The primary two advantages of this are that in many cases project
managers and/or programmers believe that useful specifications would take more
time than they’re willing to spend, and it is often difficult to come up with
useful formal specifications.
