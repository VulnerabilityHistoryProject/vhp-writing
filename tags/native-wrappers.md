Does it involve an interpreted language interacting with a native language?

Most industrial-grade languages allow for **binding** to native libraries written in other languages, such as
C. This means that, for example, a Ruby library can make a call to another library compiled in C.

This means that the vulnerabilities in native languages can still affect interpreted languages. Python, for example, isn't vulnerable to the classical forms of buffer overflow, unless native bindings are involved.