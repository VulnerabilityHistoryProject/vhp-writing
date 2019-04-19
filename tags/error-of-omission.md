An **error of omission** is when a software engineer forgot to
add functionality, as opposed to implementing existing
incorrectly. We detect errors of omission by looking at the
fix for the vulnerability: did it primarily involve *adding*
adding new functionality, or was it correcting existing
functionality?

Errors of omission are very difficult to find in a **code
inspection**. Humans' natural inclination as code inspectors
is to look for *wrong* code, not *missing* code.

Errors of omission might stem from **design issues**. Software
architecture is about delegating responsibility, and if that
responsibility is forgotten, then functionality is omitted.
For example, if your architecture dictated that you should be
checking that the existing user is root, and you forget to add
that check, then that is an error of omission. Thus, one way
to curtail this effect is to re-consult the responsibilities
of the code you are inspecting.

We tag a vulnerability as an "error of omission" for which
their fix for the vulnerability involved one of the following:

* Fixing the vulnerability involved entirely new lines of code (i.e. zero deleted lines), or
* Fixing the vulnerability involved at least a 10:1 ratio lines inserted: deleted

Note: the 10:1 ratio is completely made up and has no
reference in the academic literature. (Researchers, get on
this study... hint hint...).

We should also admit that errors of omission are a broader
concept than what this metric captures. There are likely many
more errors of omission in vulnerability history than we can
automatically identify.
