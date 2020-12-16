# [AntiCAPTCHA](http://s1063.vdi.mipt.ru:8000/challenges#AntiCAPTCHA)
Entrance for robots only. Pass special anti-CAPTCHA challenge to prove it: `nc s1063.vdi.mipt.ru 9001`

# Solution
1. After nc we receive some (100) questions. We can either try to solve all of them by hand or write python script.
```python
import sys
import socket

host = "s1063.vdi.mipt.ru" 
port = 9001

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect((host, port))


# recieve greeting 
grt = sock.recv(1024)

for i in range(100):
    # recieve quistion
    q = sock.recv(1024).decode('utf-8')
    q = q[q.find(':') + 1:q.find(' =')]

    if '/' in q:
        q = q[:q.find('/')] + '/' + q[q.find('/'):]

    # send answer
    sock.sendall(bytes(str(eval(q)) + '\n', 'utf-8'))

    #recieve answer 
    ans = sock.recv(1024)
    print(f"Test {i + 1}/100: {q} = {eval(q)}: {ans.decode('utf-8')}")

data = sock.recv(1024)
print(data)

```

**Answer**: `flag{did_you_see_leather_bastards_here?}`