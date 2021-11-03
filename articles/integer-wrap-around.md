---
title: Bad things happen when integers wrap around
author: Andy Meneely
art: rollercoaster
blurb: |
  Loop counters, file sizes, malloc arguments, session tokens, primary
  keys... numbers are everywhere in our code. What happens when our numbers get very, _very_ big?

  Integer overflow, or wraparound, is much more dangerous than it
  seems.
cves:
  - CVE-2013-4391
  - CVE-2005-2491
tags:
  - cwe-190
  - cwe-682
  - cwe-119
filepaths:
---

Loop counters, file sizes, malloc arguments, session tokens, primary keys... numbers are everywhere in our code. What happens when our numbers get very, _very_ big?

When you first learn a language like Java or C++, you almost immediately encounter integers. You can't really avoid them. But, while an integer is, mathematically speaking, infinite in possibilities, computers most certainly are not. So what happens when an integer gets too big in Java or C or C++ or many other languages? It wraps around.

This fact is often taught in introductory programming courses, but rarely is it ever talked about as a security risk. The fact is, integer overflow, or wraparound, is much more dangerous than it seems.

Let's dive into an example. In systemd's CVE-2013-4391, we had an integer that was used for computing the size of memory to be allocated on a heap. The part of the code that did this was simple enough - just logging a message as part of the `journald` logging subsystem. In `journald`, a daemon runs continuously that listens to logging messages then saves those messages according to how the system was configured. As is the practice in C, the length of the string is sent alongside the string as a separate variable, which an attacker could potentially have some influence over. The number space of the integer could exceed the size total allowable size of a log message, and this wasn't initially checked. Furthermore, if the integer wrapped around, a _smaller_ amount of space than was about to be copied would be allocated, leading to memory corruption on the heap.

The fix? Simply define a constant for how large that data chunk could be and check the size against it. What's interesting about systemd's CVE-2013-4391 is that there were two lapses by the developer: not defining a maximum size of the data chunk, _and_ not checking against that size.

The httpd project had a similar situation with CVE-2005-2491. When an untrusted user is allowed to add custom configuration through their `.htaccess` config file, which is a pretty common usage, certain regular expressions (regex) would lead to an integer wrapping around, leading to the wrong amount of memory being allocated and a potential memory corruption.

Other examples we've seen involve casting from 64-bit down to 32-bit numbers, which leads to unexpected wrapping.

Feel free to [explore some more examples in :tag:CWE-190](/tags/cwe-190) from our case studies. Similar vulnerabilities might be tagged as [:tag:CWE-119](/tags/cwe-119)] or []:tag:CWE-128](/tags/cwe-128).

Shouldn't languages throw an exception? Or give some sort of warning? That would be nice, but when you consider how much of a performance hit that would be *every* time we do arithmetic, it becomes cost-prohibitive. No, this is something many developers need to think about instead of relying upon their tech stack.

So what's the fix? How do we prevent this?

First, know your language. Every programming language, even libraries, have different ways of handling boundary cases of integer values. Javascript, for example, has the concept of a [safe integer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isSafeInteger) because of how it handles rounding. Languages like Python have popular libraries like [NumPy that have their own overflow handling](https://numpy.org/doc/stable/user/basics.types.html?highlight=s#overflow-errors) that differs from Python's native handling. Some systems will continually allocate more and more bytes to handle large numbers

Good input handling is key. Setting boundaries, allow lists, and block lists will help. But, input handling is always a good idea, but rarely your best idea.

One of the reasons we _find_ a lot of integer overflows is fuzz testing. Trying out a function with large numbers is a trivial matter for a fuzzer. So the prevalance of integer overflows in the data may be more due to our better ability to detect them compared to more subtle vulnerabilities. So if fuzz testing makes sense for your system, go for it.

Unit testing, as opposed to integration or system testing, is enormously helpful for integer overflows. Whenever you're dealing with integers be sure to attempt numbers in greater-than 32-bit space. All too often our test cases are small numbers.

And finally, from a vigilance standpoint, pay attention to when you're doing something important (like allocating memory) with a number, and then ask _what would happen if this number wrapped around?_.