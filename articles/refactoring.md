---
title: Always Be Refactoring
author: Andy Meneely
art: refactor
blurb: |
  You can't secure it if you can't maintain it.

  Refactoring is the practice of improving the maintainability of the code 
  without changing its functionality. Problems can occur when refactoring is ignored for long periods of time. 

  Refactoring is an active area of software engineering research.

cves:
tags:
filepaths:
---
You can't secure it if you can't maintain it.

A widespread practice, refactoring is useful for improving your code's **maintainability**. If you are changing the code without changing what it _does_, you are refactoring. Simple refactorings include:

* Renaming a variable, method, class, etc.
* Extract a chunk of code into a separate method, class, etc.
* Inlining code from an existing method
* Moving code to a more intuitive place

You can see a larger catalog at [refactoring.com](https://refactoring.com/catalog/). Much of the original refactoring work is credited to Martin Fowler.

Refactoring is also much easier when the system has an [automated regression test suite](/articles/automated-testing). Regression testing allows you to make changes and have some guarantees that you are performing the same functionality. They make changes to your code safer. 

A refactoring effort can also be preparation for a significant change like an architectural change or a new feature. For example, you could take a chunk of code and refactor it out to another method as a way to generalize it for others to use it. 

In research, the relationship between bugs and refactoring is quite clear. An [October 2020 study from Pantiuchina et al.](https://doi.org/10.1145/3408302) shows that developers have a variety of reasons behind their refactoring efforts. Here are several prominent reasons, summarized from Table 7:

* Improve Code Design
* Improve Understandability and Readability
* Improve Quality of Test Code
* Preparing for Code Changes
* Prevent bugs
* Improve Performance
* Promote API compatibility

The relationship between vulnerabilities, specifically, and refactoring is an [open question](/articles/open-question). What refactoring techniques are most commonly associated with secure software? Does a history of regularly applying refactoring to code correlate with a lower rate of vulnerabilities? We believe this area of research needs to be explored.

Below are some more studies on refactoring:

* Jevgenija Pantiuchina, Fiorella Zampetti, Simone Scalabrino, Valentina Piantadosi, Rocco Oliveto, Gabriele Bavota, and Massimiliano Di Penta. 2020. Why Developers Refactor Source Code: A Mining-based Study. ACM Trans. Softw. Eng. Methodol. 29, 4, Article 29 (October 2020), 30 pages. [https://doi.org/10.1145/3408302](https://doi.org/10.1145/3408302)
* Mohammad Alshayeb. 2009. Empirical investigation of refactoring effect on software quality. Inf. Softw. Technol. 51, 9 (2009), 1319--1326. 
* Gabriele Bavota, Andrea De Lucia, Andrian Marcus, and Rocco Oliveto. 2013. Using structural and semantic measures to improve software modularization. Empir. Softw. Eng. 18, 5 (2013), 901--932.
* Gabriele Bavota, Andrea De Lucia, Massimiliano Di Penta, Rocco Oliveto, and Fabio Palomba. 2015. An experimental investigation on the innate relationship between quality and refactoring. J. Syst. Softw. 107 (2015), 1--14. [https://doi.org/10.1016/j.jss.2015.05.024](https://doi.org/10.1016/j.jss.2015.05.024)
* Raymond P. L. Buse and Westley Weimer. 2010. Learning a metric for code readability. IEEE Trans. Softw. Eng. 36, 4 (2010), 546--558.
* Dawn Lawrie, Christopher Morrell, Henry Feild, and David Binkley. 2007. Effective identifier names for comprehension and memory. Innov. Syst. Softw. Eng. 3, 4 (2007), 303--318.



