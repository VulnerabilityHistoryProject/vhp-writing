Did the fix lack automated testing?

**Automated testing** is an invaluable practice that can help prevent regressions, help document your code's behavior, and ensure quality as you develop.

They are also a _ton_ of work. Maintaining a robust unit test suite takes discipline and devotion. And the tests are only as good as the developer: the test suite will have the same blind spots as the person who wrote them.

When examining a vulnerability, we asked curators to examine if the code fixed for a vulnerability involved some sort of automated testing. This tag was for when the **fix did not include** an updated unit test.

One of the key values of a automated tests is that they ensure that a specific mistake will never happen again, so one would hope to see a lot of vulnerability fixes involve updating unit tests. On the other hand, developers fixing a vulnerability might be rushed and might be inclined to circumvent their usual quality assurance practices.