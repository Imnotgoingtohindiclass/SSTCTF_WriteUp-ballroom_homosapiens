# sstudents 2
**Difficulty: Advanced**
### Challenge:
I can't login to my account... can you help me?

https://web4-sst.ybn.sg/

## Solution:
A classic case of SQL Injection.
SQL injection is one of the most common web hacking techniques, where you place malicious code in SQL statements, via web page input.
SQL injection usually occurs when you ask a user for input, like their username/userid, and instead of a name/id, the user gives you an SQL statement that you will unknowingly run on your database.
Just input `1 OR 1=1`. The SQL here is valid and will return the flag since `OR 1=1` is always TRUE.
This will get the flag **sstctf{}**.