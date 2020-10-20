---
title: What is a VCC?
author: Andy Meneely
art: ice-cream-spill
blurb: |
  A **Vulnerability-Contributing Commit** is the change to source code that is likely the origin of a vulnerability.

  Finding a VCC is our attempt at finding the original mistake that was made... and missed... that led to a vulnerability.
cves:
tags:
  - lifetime-30d
  - lifetime-3mo
  - lifetime-90d180d
  - lifetime-180d1y
  - lifetime-1y2y
  - lifetime-2y5y
  - lifetime-5y
filepaths:
---

_When did this first start?_

_What was the original mistake made that led to this problem?_

These are key questions in any post-mortem discussion. To find some answers, we look to version control systems such as Git. Since every minute change to the system is tracked in a large project, we can know when a chunk of code was introduced. The feature that uses these is typically called a `blame` or an `annotate` (e.g. `git blame`). 

Software engineering researchers have long used an adapted version of the blame algorithm called the [SZZ algorithm](https://doi.org/10.1145/1082983.1083147) to identify what commits contributed to the problem. Given a commit that we accept as being the fix for a bug, the SZZ algorithm identifies the commit(s) that first introduced those lines of code.

Other methods exist for this, however, the SZZ algorithm has gained popularity because it's easy to execute. For vulnerabilities, we coined the term "Vulnerability-Contributing Commit" (VCC) in [our earlier work](https://doi.org/10.1109/ESEM.2013.19), which since been adopted by other researchers. Some researchers call them "bug-inducing commits" or "fix-inducing changes" or the like, although we prefer the word "contribute" over "induce".

Automatically identifying a VCC is not without its faults. Here are three issues with it: 

* **It's just text.** The `blame` feature has no awareness of the programming language - it is merely comparing text. This means that if the fix or VCC involves correcting comments, or other [refactorings](/articles/refactoring), then we may get a false positive. 
* **Checking code statically, not verifying behavior**. Identifying the algorithm is not attempting to confirm
* **Where to fix something is subjective**. When you fix a bug in code, you often have many choices on how to fix it. Do you fix in the presentation layer, or in the database schema? Do you simply filter the bad output, or redesign the module? Or just rip out the feature entirely? For us, we assume that if the development team has a commit that they identify as a fix, then the code they correct is assumed to be "wrong", even though the notion of "wrong" is a subjective one. (Does your brain hurt yet?)

In this project, we use a combination of the SZZ algorithm [and its variants](https://github.com/samaritan/archeogit) to identify VCCs, then ask our curators to confirm. By having a human look at a VCC and fix, they can see refactorings that can be disregarded or any other potential issues. This helps mitigate some of the the above issues to some extent, and this approach goes much farther than the current academic literature (that we know of). 


