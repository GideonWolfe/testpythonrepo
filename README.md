# testpythonrepo

The problem I am trying to solve is how to organize my code well without dealing with import statement hell.

Here is the current layout of this toy repo:

```
testpythonrepo/
├── package
│   ├── subdir1
│   │   ├── hello.py
│   │   └── __init__.py
│   ├── subdir2
│   │   ├── __init__.py
│   │   └── world.py
│   ├── driver.py
│   └── __init__.py
└── README.md
```

With the above layout, I try something like this in `driver.py`, but I get these errors thrown at me.

![](https://i.imgur.com/HZhWV1y.png)

However, just running `python3 driver.py` prints out both words as you would expect. 

When I edit the file like so to include `package` before, the error disappears in `nvim`. 

![](https://i.imgur.com/4p3Csht.png)

But when I actually try `python3 driver.py`, of course I get 

```
Traceback (most recent call last):
  File "driver.py", line 2, in <module>
    from package.subdir2.world import printWorld
ModuleNotFoundError: No module named 'package'
```
