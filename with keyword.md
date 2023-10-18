Resources:
- [with keyword](https://builtin.com/software-engineering-perspectives/what-is-with-statement-python)

Use: The `with` statement is a replacement for commonly used `try/finally` error-handling statements.

`with`:
``` python
with open("example.txt", "w") as file:
    file.write("Hello World!")
```
no `with`:
``` python
f = open("example.txt", "w")

try:
    f.write("hello world")
finally:
    f.close()
```

