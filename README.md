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

Why is the error checking the opposite of reality?

Another thing I am going to need to be able to do is call functions that are in separate subdirectories. In this context, say I wanted to call `printWorld()` directly from
`printHello()`, so driver only had to call `printHello()` in order for `Hello World` to be printed.

In `hello.py`, I do

![](https://i.imgur.com/jS8qy3s.png)

No error on the import line, but lo and behold 

```
Traceback (most recent call last):
  File "driver.py", line 1, in <module>
    from subdir1.hello import printHello
  File "/home/gideon/test/testpythonrepo/package/subdir1/hello.py", line 1, in <module>
    from ..subdir2.world import printWorld
ValueError: attempted relative import beyond top-level package
```

when I try to run `driver.py` directly


# TL;DR

What am I doing wrong here? I simply want to;

* Get files to call each other from across directory levels
* Get `neovim`/`coc-python` to stop throwing false errors

Please feel free to submit a PR or issue with any fix
