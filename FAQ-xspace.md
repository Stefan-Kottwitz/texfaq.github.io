# Commands gobble following space

People are forever surprised that simple commands gobble the space
after them: this is just the way it is.  The effect arises from the
way TeX works, and Lamport describes a solution (place a pair of braces
after a command's invocation) in the description of LaTeX syntax.
Thus the requirement is in effect part of the definition of LaTeX.

These FAQs,
for example, is written in LaTeX for production of a web site.  The
HTML code is generated by a script that _requires_ a pair of
braces, to make a null argument, as in:
  `\fred{}` 
for almost all macro invocations, regardless
of whether the following space is required: however, these FAQs
should not itself be regarded as a model of LaTeX style.

Many users find all those braces become very tedious very
quickly, and would really rather not type them all.

An alternative structure, that doesn't violate the design of LaTeX,
is to say `\fred``\ `&nbsp;&mdash; the `\ ` command is ''self
terminating'' (like ` `) and you don't need braces after
_it_.  Thus one can reduce to one the number of extra characters
one needs to type.

If even that one character is too many, the package [`xspace`](http://ctan.org/pkg/xspace)
defines a command `\xspace` that guesses whether there should have
been a space after it, and if so introduces that space.  So
`fred`\xspace` jim` produces ''fred jim'', while
`fred`\xspace`. jim` produces ''fred. jim''.  Which
usage would of course be completely pointless; but you can incorporate
`\xspace` in your own macros:
```latex
\usepackage{xspace}
...
\newcommand{\restenergy}{\ensuremath{mc^2}\xspace}
...
and we find \restenergy available to us...
```
The `\xspace` command must be the last thing in your macro
definition (as in the example); it's not completely foolproof, but it
copes with most obvious situations in running text.

The [`xspace`](http://ctan.org/pkg/xspace) package doesn't save you anything if you use it in
a macro that appears only once or twice within your document, and it
is not totally foolproof.  (The original author of the package wrote
it because he had been bitten by lost spaces.  He no longer recommends
its use, simply because of the possibility of error.)

In any case, be
careful with usage of `\xspace`&nbsp;&mdash; it changes your input syntax,
which can be confusing, notably to a collaborating author
(particularly if you create some commands which use it and some which
don't).  No command built into LaTeX or into any
''standard'' class or package will use `\xspace`.
