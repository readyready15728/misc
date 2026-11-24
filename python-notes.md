# Python Notes

## `from __future__ import brackets`

* The warning in chapter 2 of _Time Series Forecasting with Python_ when
setting the historical mean in the `test` data frame by copying like so:
`test = df.copy()[-4:]`.
* The assignment of `pred_last_season` in the same chapter uses `.values`
because of the different indexing of the data.
* `df[pd.to_datetime(df['Date']).dt.month == 5]` used with `GOOGL.csv` can be
used to determine to the first matching index with the month of May and so
forth.
* `df.loc[450:, 'pred_widget_sales'] = (df['widget_sales'].iloc[450] +
pred_df['pred_MA'].cumsum()).values` is needed to conform with pandas 3.0
expectations.
* For the Kaggle tutorial on Pandas: `top_oceania_wines =
reviews.loc[(reviews['country'].isin(('Australia', 'New Zealand'))) &
(reviews['points'] >= 95)]`.
* `bargain_wine = reviews.iloc[(reviews['points'] /
reviews['price']).idxmax()]['title']`.
* Here is a solution a bit more general than the suggested one looking for keywords in wine reviews:

```python
keywords = ['tropical', 'fruity']
descriptor_counts = pd.Series([reviews['description'].map(lambda desc: keyword in desc).sum() for keyword in keywords], index=keywords)
```
* Consider using `:-` in the future.
* Remember the optional `else` block available with `for` and `while` loops.
* Using iterator-based `for` loops with file objects runs at C-language speed
in standard CPython whereas a `while` loop using `.readline()` runs in the
Python virtual machine and is likely to be slower. And `.readlines()` is just
inefficient, putting the entire file contents into memory at worse.
* An iterable returns an iterator when `iter()` (or, really, `.__iter__()` is
called. The iterator then implements the following protocol: `next()` (or
`.__next__()` to get the next object in the iterator and raises the exception
`StopIteration` when no more results remain, and is the same as calling
`next()`.
* Here's an [article about how to avoid callbacks made in loops from using the
last value of the loop](https://www.bobobk.com/en/python-loop-callback-late-binding.html).
* `map()` can take multiple iterables.
* The `operator` module can be useful for functional programming. Consider the
following, which avoids the use of a `lambda`:
```python
from functools import reduce
from operator import mul

def factorial (n):
    return reduce(mul, range(1, n + 1))
```
* Generators can be effectively infinite. Fibonacci numbers might be
illustrative. In fact, here it is:

```python
def fib():
    i, j = 0, 1
    n = 0

    while True:
        if n < 2:
            if n == 0:
                yield 0
            else:
                yield 1
        else:
            i, j = j, i + j
            yield j
      
        n += 1
```
* Use `list(str_variable)` instead of what I seem to remember using,
`str_variable.split('')`. (Doesn't even work as of Python 3.12.)
* Use `collections.namedtuple` for lightweight immutable record objects with
named fields.
* If the result of `.__repr__()` is user-friendly, `str()` will use it if
`.__str()__` is not available. If you implement only one of these two dunder
methods, make it `.__repr__()`.
* Be mindful of the different options now available with iterable unpacking.
* Slices in mutable sequences can be assigned, not just accessed. In such
instances, `del` also works.
* If `.__iadd__()` or `.__imul()__()` are not implemented, Python will fall
back on `.__add__()` or `.__mul__()`, respectively.
* Python has a module supporting binary search and keeping lists suitable for
binary search called `bisect`.
* "The `list` type is flexible and easy to use, but depending on specific
requirements, there are better options. For example, an `array` saves a lot of
memory when you need to handle millions of floating-point values. On the other
hand, if you are constantly adding and removing items from opposite ends of a
list, it’s good to know that a `deque` (double-ended queue) is a more efficient
FIFO data structure."
* `ChainMap` from module `collections` might be useful for implementing an
interpreter for a language with nested scopes, from the innermost enclosing
scope to the outermost.
* Here's a Reddit thread called [What hidden gem Python modules do you use and why?](https://www.reddit.com/r/Python/comments/1rrz3kx/what_hidden_gem_python_modules_do_you_use_and_why/).
* A Hackernews posted about [Lesser known parts of the Python standard
library](https://news.ycombinator.com/item?id=41450824).
