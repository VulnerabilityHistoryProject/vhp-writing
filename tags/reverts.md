The vulnerable code had a lot of reverts in its lifetime

A vulnerability with this tag has had at least 10 separate weeks where at least one commit mentioned the word "revert" in the commit message.

Reverting code is a feature of Git that allows you to completly reverse a prior commit. We believe that code with a history of frequent reverts might be indicative that the code owners are too eage to merge in changes without careful review. This hypothesis is untested, but we are curious.