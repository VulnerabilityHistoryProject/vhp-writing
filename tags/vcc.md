Do we have a vulnerability-contributing commit on record?

A **vulnerability-contributing commit** is a commit that we believe is the origin of a vulnerability in source control. If a vulnerability has this tag, then we have found at least one VCC for it.

We use a modified version of the [SZZ algorithm](https://dl.acm.org/doi/abs/10.1145/1082983.1083147) using the [archeogit](https://github.com/samaritan/archeogit) built by Nuthan Munaiah to identify VCCs. In short, this algorithm uses `git blame` functionality to trace individual lines of code back to their origins. Curators are asked to verify if the VCCs are valid, so these have manual curations as well.