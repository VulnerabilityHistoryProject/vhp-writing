Did it involve environment variables?

**Environment variables** are useful tools for allowing a process to be configurable without having to store secrets in file systems or elsewhere. The practice of using environment variables, when done properly, is considered to be a good one.

However, environment variable behavior can vary across platforms (e.g. case sensitivity) and are an oft-overlooked part of the attack surface. Sometimes a fix for a vulnerability will involve adding a new configuration, which can impact environment variables. Finally, environment variables are often the source of important information which can leak out through error messages, as in [:tag:CWE-209](/tags/cwe-209).

