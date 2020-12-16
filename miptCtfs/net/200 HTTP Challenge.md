# [HTTP Challenge](http://s1063.vdi.mipt.ru:8000/challenges#HTTP%20Challenge)

How does [HTTP](http://chall1.ctf.pwne.xyz:9005/) work?

Hint: it may require requests module for python or netcat utility.

# Solution

## HTTP Challenge (level 1)

[Link](http://chall1.ctf.pwne.xyz:9005/70a17f25-a6e0-4c23-8a1b-5786038c0527/)

Your target: Execute GET request with arguments: f00=b4r and y3t_an0th3r=GET_ARG

### Solution

`http://chall1.ctf.pwne.xyz:9005/70a17f25-a6e0-4c23-8a1b-5786038c0527/?f00=b4r&y3t_an0th3r=GET_ARG`

## HTTP Challenge (level 2)

[Link](http://chall1.ctf.pwne.xyz:9005/962a7c1e-1e21-4f21-ba27-7d4b84f31062/)

Your target: Execute POST request with arguments: f00=b4r and y3t_an0th3r=POST_ARG

### Solution 

```python
from requests import post

url = 'http://chall1.ctf.pwne.xyz:9005/962a7c1e-1e21-4f21-ba27-7d4b84f31062/'
data = {'f00': 'b4r', 'y3t_an0th3r': 'POST_ARG'}
res = post(url, data=data)
print(res.text)
```

## HTTP Challenge (level 3)

[Link](http://chall1.ctf.pwne.xyz:9005/ad8c7b1f-aeca-49e7-ac1b-3d4812f5b49b/)

Your target: Your User-Agent should be equals 'Sup3rSecr3tUser4gent'

### Solution 

```python
from requests import get

url = 'http://chall1.ctf.pwne.xyz:9005/ad8c7b1f-aeca-49e7-ac1b-3d4812f5b49b/'
headers = {
    'User-Agent': 'Sup3rSecr3tUser4gent'
}
res = get(url, headers=headers)
print(res.text)
```

## HTTP Challenge (level 4)

[Link](http://chall1.ctf.pwne.xyz:9005/3b27f25a-a146-40f4-bb1c-519b01470bb5/)

Your target: Your server protocol should be equals 'HTTP/0.1'

### Solution

`$ printf "GET /3b27f25a-a146-40f4-bb1c-519b01470bb5/ HTTP/0.1\r\n\r\n" | nc chall1.ctf.pwne.xyz 9005`

## HTTP Challenge (level 5)

[Link](http://chall1.ctf.pwne.xyz:9005/5312fc8c-af1a-4556-a8e4-6ba41c894a92/)

Your target: Your HTTP method should be equals 'FLAG'

### Solution 

`$ printf "FLAG /5312fc8c-af1a-4556-a8e4-6ba41c894a92/ HTTP/0.1\r\n\r\n" | nc chall1.ctf.pwne.xyz 9005`

[Final link](http://chall1.ctf.pwne.xyz:9005/3572e913-6fd0-43fa-a3b4-3afac955a746/)

**Answer**: `flag{HTTP_Is_4_pRettY_c00l_pR0tocol}`