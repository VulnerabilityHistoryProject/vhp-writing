---
title: Beware of complex inputs
author: Andy Meneely
art: snowflake
blurb: |
  Don't just think about code complexity, think about *input* complexity.
cves:
  - CVE-2015-1296
  - CVE-2011-2850
  - CVE-2008-0005
  - CVE-2011-3045
  - CVE-2016-5152
  - CVE-2015-6781
tags:
  - complex-inputs
  - least-privilege
  - defense
filepaths:
---

Computers only understand numbers, so the ways in which we translate our inputs are quite elaborate. If your inputs are complex, errors will abound.

We have a tag, called [:tag: Complex Inputs](/tags/complex-inputs) where we've found examples of this. Let's run through a couple of interesting ones:

**URLs** are complex. In CVE-2015-1296, what we've nicknamed "Lock-Alike", there was a vulnerability in the Chromium browser in the way URLs were handled in the address bar. By manipulating how bidirectional text is rendered, and by embedding emojis, someone could spoof an SSL padlock.

**Unicode** is complex. In CVE-2011-2850, we see that a mishandling of the Khmer characters led to a memory buffer out-of-bounds read. The unit tests that examined this vulnerability attempted many different languages, but having a single Khmer character would cause the string allocation to go wrong, leading to a buffer overflow.

In CVE-2008-0005 we saw auto-detection go wrong when the Apache server would assume that some inputs were the wrong character set and attackers could forge their own delimiters.

**Images** are complex. In CVE-2011-3045 we saw how PNGs can be specially crafted to trigger integer overflows in Chromium that led to a decompression bomb. When developers are testing complex inputs like images, they will often generate those images using _another set of good-faith tools_. For example, they might use Photoshop to generate a PNG file. Knowing how to hand-craft a PNG file is far beyond the skill level of most developers (it certainly is not part of a standard SE or CS college curriculum!). Another similar version of this was CVE-2016-5152, only with JPEG.

**Fonts** are complex. You might not realize it, but fonts need to both be fast and hyper-customizable. Vulnerabilities like CVE-2015-6781 have come from parsing font files that are filled with esoteric typographical metrics, vector drawings, alias hinting, and code point tables.

How should we defend against complex inputs? There's a lot to say about it, but it's a combination of thorough testing and a combination of block-lists and allow-lists.


