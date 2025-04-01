# Hidden in Discord
**Difficulty: Hard**
### Challenge:
Mr Pang 曾经说过，“我们可以编写出非常好的代码，但总会有糟糕的用户。“
nc shuttle.proxy.rlwy.net 26784

## Solution:
A classic case of input vulnerability. Looking at the code:
```python
flag = 'sstctf{REDACTED}'

number = input('Enter a number: ')
if number.isnumeric():
    try:
        number = int(number)
        print(number)
    except ValueError:
        print('Why are you such a bad user?')
        print(flag)
else:
    print('Input validation failed!')
```
The code require us to input a value that passses through `.isnumeric()` but not `int()` function such that we trigger `ValueError`.
The `isnumeric()` method returns True if all the characters are numeric (0-9), otherwise False. Exponents, like ² and ¾ are also considered to be numeric values.
However, such values cannot be used in the `int()` function. Hence, the function fails and a `ValueError` error pops up.
To achieve this, the above values or any other language that represents a number should suffice. An example would be 三. Inputting that character will give you the flag **sstctf{}**.