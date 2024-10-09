# Python Notes
## from __future__ import brackets

* The warning in chapter 2 of _Time Series Forecasting with Python_ when
setting the historical mean in the `test ` data frame by copying like so:
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
