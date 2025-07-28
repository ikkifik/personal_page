---
layout: posts
title: "Kaggle: Pandas"
date: 2025-07-26
category: Learning-notes
---
- DataFrame is a table
	`pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})`
- Series is a single column of a DataFrame, it forms a list
	`pd.Series([1, 2, 3, 4, 5])`

- Meaning of this `(129971, 14)` when running command `df.shape `is "*a DataFrame has 130,000 records split across 14 different columns, which almost 2 million entries*"

- `iloc` -> index-based selection, 
	- to call starts from `[row, column]`
	- `reviews.iloc[:, 0]` to retrieve all rows of the first column
	- `reviews.iloc[:3, 0]` to retrieve rows from first(0) to third(2), fourth (3) not counted
	- `reviews.iloc[1:3, 0]` to retrieve rows from 2nd(1) and 3rd(2)
	- `reviews.iloc[-5:]` to retrieve the last 5 rows

- `loc` -> label-based selection
	- `reviews.loc[0, 'country']` to retrieve the first row of country column
	- by the course, it considered simpler using `iloc` compared to `loc`, because it uses index position instead. But `loc` provide easier ways to do things since it uses column name.
	- `reviews.loc[reviews.country == 'Italy']` -> use `loc` for conditional selection
	- `reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]` for more than 1 condition, use the ampresand (`&`) symbol, just like SQL but it's only 1.
	- for `or` we can change it to single pipe (`|`) symbol
	- `reviews.loc[reviews.country.isin(['Italy', 'France'])]` to select *country* rows that states only *Italy* and *France* values.

- From course: 
	- *`iloc` uses the Python stdlib indexing scheme, where the first element of the range is included and the last one excluded. So `0:10` will select entries `0,...,9`.*
	- *`loc`, meanwhile, indexes inclusively. So `0:10` will select entries `0,...,10`.*

- Assigning data:
	- constant data: `reviews['critic'] = 'everyone'`
	- continuous data: `reviews['index_backwards'] = range(len(reviews), 0, -1)`

- `Map` function -> it uses a single value from the **Series** and return a transformed version of that value, for example `reviews.points.map(lambda p: p - 10)` it means the `points` column value will be reinterpreted as `p` subtracted with `10 `for the whole rows.

- `Apply` function -> similarly with `map` by function, what makes it differs is `apply` uses calling a custom method/function for each row and transform the whole **DataFrame**, for example `reviews.points.apply(some_method_name, axis='columns')`

- To note, those 2 doesn't change the original dataset.
