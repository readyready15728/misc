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
* An iterable returns an iterator when `iter()` (or, really, `__iter__()` is
called. The iterator then implements the following protocol: `next()` (or
`__next__()` to get the next object in the iterator and raises the exception
`StopIteration` when no more results remain, and is the same as calling
`next()`.
* Test.
