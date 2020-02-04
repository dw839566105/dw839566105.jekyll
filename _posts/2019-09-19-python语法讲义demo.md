---
layout:     post
title:      python简单语法
subtitle:   
date:       2019-09-20
author:     BY DW
header-img: img/post/post-bg-2.jpg
catalog: true
tags:
    - python
---

> 参考内容 [Dive into python](https://diveintopython3.problemsolving.io/)  
> 参考内容 [Runoob 教程](https://www.runoob.com/python3/python3-tutorial.html)

# 0. Installing python

# 1. Function
## 1.1 First python program
>  
    SUFFIXES = {1000: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],
    1024: ['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']}
    
    def approximate_size(size, a_kilobyte_is_1024_bytes=True):

        '''Convert a file size to human-readable form.
        Keyword arguments:

        size -- file size in bytes
        a_kilobyte_is_1024_bytes -- if True (default), use multiples of 1024
        if False, use multiples of 1000

        Returns: string
        '''
        if size < 0:
        raise ValueError('number must be non-negative')
        multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
        for suffix in SUFFIXES[multiple]:
            size /= multiple
            if size < multiple:
                return '{0:.1f} {1}'.format(size, suffix)
        raise ValueError('number too large')

    if __name__ == '__main__':
        print(approximate_size(1000000000000, False))
        print(approximate_size(1000000000000))
function format:
>
    def func_name(var1, var2 = v2, *args, **kargs)
        '''
        fun.__doc__
        '''
        Your code here

        return value

Note:   
> 1. Use `'''  '''` to include instruction of functions, which is shown in `fun.__doc__`
> 2. The `fun.__name__` is `__main__` Only when the program is being executed, it will not be executed when be imported 
> 3. Python use <kbd>tab</kbd> to promise a block, not `end` or `{}`
> 4. `*args` likes a tuple, passing par values
> 5. `**kargs` likes a dic, passing key values and names
> 6. `func.__self__`

Everything is object: 
Use `type()` or `.type` to view the class of variable.
> 1. SUFFIXES: dictionary
> 2. SUFFIXES[index]: list
> 3. approximate_size: function
> 4. print: built-in function

Variables:
``` 
    >>> from humansize import approximate_size
    >>> approximate_size(4000, a_kilobyte_is_1024_bytes=False)
    '4.0 KB'
    >>> approximate_size(size=4000, a_kilobyte_is_1024_bytes=False)
    '4.0 KB'
    >>> approximate_size(a_kilobyte_is_1024_bytes=False, size=4000)
    '4.0 KB'
    >>> approximate_size(a_kilobyte_is_1024_bytes=False, 4000)
    File "<stdin>", line 1
    SyntaxError: non-keyword arg after keyword arg
    >>> approximate_size(size=4000, False)
    File "<stdin>", line 1
    SyntaxError: non-keyword arg after keyword arg
```
As soon as you have a named argument, all arguments to the right of that need to be named arguments, too.  


