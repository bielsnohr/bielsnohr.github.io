---
layout: post
title:  "Decorators to Time Functions in Python"
tags: courses software-engineering
---

After a hiatus from blog writing, I am finally getting back on the horse. It
has been a tough year for us all, so I feel no shame for not being as
consistent as I would like to be. Anyway, now for the technical stuff.

Quite some time ago while I was working on the [Google Tech Dev
Guide]({% post_url 2020-06-19-google-tech-dev-guide %}) I wanted to get some
performance information about some of the algorithms I was implementing. I was
surprised to find that Python doesn't have an immediately obvious way to do
this.

There is the
[timeit](https://docs.python.org/3/library/timeit.html#module-timeit) module in
the Standard Library, but my initial reading and attempted use seemed to
indicate that you cannot use your own functions with this module, which would
render it pretty useless in my view. Unfortunately for past me, there is an
important piece of information buried at the bottom of the module webpage that
I only noticed just now:

> To give the timeit module access to functions you define, you can pass a
> setup parameter which contains an import statement:
> 
> ```python
> def test():
>     """Stupid test function"""
>     L = [i for i in range(100)]
> 
> if __name__ == '__main__':
>     import timeit
>     print(timeit.timeit("test()", setup="from __main__ import test"))
> ```
> 
> Another option is to pass globals() to the globals parameter, which will
> cause the code to be executed within your current global namespace. This can
> be more convenient than individually specifying imports:
> 
> ```python
> def f(x):
>     return x**2
> def g(x):
>     return x**4
> def h(x):
>     return x**8
> 
> import timeit
> print(timeit.timeit('[func(42) for func in (f,g,h)]', globals=globals()))
> ```

In hindsight, I probably would have used the latter option of passing
`globals()` to the `timeit.timeit()` function call for my purposes. However,
not discovering this at the time forced me to look for other options. The one
that appealed to me most was the suggestion of using a decorator in [this
RealPython article](https://realpython.com/python-timer/).

Here is my implementation:

```python
import functools
import time

def timer(number=10000):
    """Decorator that times the function it wraps over repeated executions

    Parameters
    ----------
    number : int
        The number of repeated executions of the function being wrapped
    Returns
    -------
    func
    """
    def actual_wrapper(func):
        @functools.wraps(func)
        def wrapper_timer(*args, **kwargs):
            tic = time.perf_counter()
            for i in range(number - 1):
                func(*args, **kwargs)
            else:
                value = func(*args, **kwargs)
            toc = time.perf_counter()
            elapsed_time = toc - tic
            print(f"Elapsed time of {func.__name__} for {number} runs:\n"
                  f" {elapsed_time:0.6f} seconds")
            return value
        return wrapper_timer
    return actual_wrapper
```

The extra level of function definitions compared to the usual decorator
definition is necessary so that the decorator can take an argument. You can
stick this code in a Python module and import it in any project when you want
to time the functions you are writing. Better yet, I should package it on PyPI
for broader use.

I like the flexibility that the decorator offers and the fact that you can
retain the normal function calls that you would be making anyway. I think the
next step would be to add some way to switch timing on and off, although I
don't know whether that is even possible with this decorator implementation.
Worth a ponder!
