Is this an example of the **Frameworks are Optional** lesson?

> We aren't vulnerable to SQL injection because we use an object-relational mapper!
>   - Someone who is wrong

Modern software development often relies on building with an existing library of methods and data structures, often called a **framework**. Examples can include Ruby on Rails, Django, or Unity. These frameworks give you a host of tools at your disposal and will fix many, many security problems for you if you ask them to. 

But there's always a way to bypass the framework and do what you want. 

After all, Ruby on Rails is still Ruby, and Django is still Python. When the framework doesn't developers what they want, developers find a way around it. This is why *adopting a framework is a mitigation*, not an elimination. And certainly not an excuse to learn about the vulnerabilities that the framework is trying to prevent for you.