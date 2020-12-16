# [netdog](http://s1063.vdi.mipt.ru:8000/challenges#netdog)
Just use netcat: `nc s1063.vdi.mipt.ru 9000`

# Solution
1. `$ nc s1063.vdi.mipt.ru 9000`
```
Flag? (y/n)
> y
[*] Resolving whitehouse.gov...  Done!
[*] Connecting to 152.257.53.14:75274...  Done!
[*] Leaking heap address...  Done! (0x5644af57a000)
[*] Leaking libc base address...  Done! (0x7fc3e60a7000)
[*] Trying to patch mallochook...  Done! (Failed)
[*] Trying to pivot stack...  Done! (Success)
[*] Preparing ROP-chain...  Done!
[+] Got shell!
[*] Looking for flag...
[+] Flag: flag{hack^Wnc_the_world}
```

**Answer**: `flag{hack^Wnc_the_world}`