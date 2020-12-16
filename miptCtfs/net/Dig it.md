# [Dig it](http://s1063.vdi.mipt.ru:8000/challenges#Dig%20it) 
This domain hides something: `flag.x.pwne.xyz`. Help me to dig true.

# Solution

`$ dig flag.x.pwne.xyz  TXT`

```
; <<>> DiG 9.11.23-RedHat-9.11.23-1.fc33 <<>> flag.x.pwne.xyz TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23371
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;flag.x.pwne.xyz.		IN	TXT

;; ANSWER SECTION:
flag.x.pwne.xyz.	185	IN	TXT	"flag{dig_1t_plz!1}"

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sat Nov 07 14:53:26 MSK 2020
;; MSG SIZE  rcvd: 75
```

**Answer**: `flag{dig_1t_plz!1}`