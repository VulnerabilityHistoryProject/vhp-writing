---
title: "Let's Just Undo That"
author: Andy Meneely
art: revert
blurb: |
  A revert is when a commit is reversed, indicating that developers have decided to roll back changes that were
  originally approved and integrated into the system.
cves:
  - CVE-2016-5159
  - CVE-2016-1647
tags:
  - reverts
filepaths:
---

Source code control is a beautiful thing. Software engineering would be impossible with out tools like Git that allow thousands of people to collaborate around the world.

One of the useful features of Git is `git revert`. As described in the [Git documentation](https://git-scm.com/docs/git-revert), `git revert` allows you to essentially reverse the actions of a previous commit. If you look at a patch that was a revert, it will be the exact opposite of the patch it was reverting. It's a new commit, just reversing the work.

What's so bad about that?

In isolation, nothing. But let's step back and think about the life of an open source developer. You work tirelessly on a system that many depend on, but few understand. One day you get a pull request! How exciting - someone took the time to understand your system, your code, and found a way to improve it. You want more work from them, of course, so you allow it into your system. They contributed to a part of the system you consider to be pretty stable, and you're focusing on other things, so it's nice to get the help.

But then, later on, you find that, as anyone is when they're first contributing to a new system, the patch has problems. You could (a) dig into the code that someone else wrote, or (b) simply reverse back to a known state. The latter option is going to be faster and you know the system is stable without it. So instead of continuing to _improve_ the code they contributed, you simply `git revert` and go back to a stable world.

In that scenario, the developer had _two_ opportunities to review and improve the code. First, when the initial contribution was made, and second when the problems were uncovered. Instead, both opportunities were skipped and the system remained where it started.

Put more simply, a consistent pattern of `git revert` commits could be a symptom of a process problem.

Here are some examples. In CVE-2016-5159, we see that the vulnerable code went through 302 revert commits in a 7 year period, averaging 3.5 per month or nearly one per week. Most of those can be attributed to the `DEPS` file that defined the dependencies, which introduced many challenges for Chromium developers.

In CVE-2016-1647, we saw 8 revert commits in the span of 8 months during the lifetime of the vulnerability, and 47 revert commits in the six years of the vulnerable code's lifetime. Looking at the timeline the reverts were part of the regular habit of the project, i.e. not from a single event. One of those files, [render_widget_host_impl.cc](/filepaths/chromium-content-browser-renderer_host-render_widget_host_impl-cc), has been fixed for four vulnerabilities alone.

There can be many great reasons for using `git revert`. It's a great feature! But we have noticed that the histories of many vulnerabilities involve a lot of `git revert` commits. We don't have any proof of this (hello, SE researchers!), but we believe that having a history of many reverts might indicate a deeper, systemic issue with  **lacking a continuous improvement** mindset.

Researchers are beginning to look at this. A study at by [Wen et al. at _Empirical Software Engineering 2022_](https://link.springer.com/article/10.1007/s10664-021-10051-z) explored the topic of "quick remedy" commits in repositories and how that impacts other mining studies.