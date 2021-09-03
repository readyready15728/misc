# R Notes
## Notes on the powerful but often confusing statistical computing package

* Only `&` and `|` are vectorized logical operators; attempting to use `&&` or
  `||` on a vector will likely not result in the desired outcome.
* The code at the bottom of page 178 in *Practical Machine Learning in R*
  didn't work. Here's what did:

  ```r
  donors <- donors %>%
  mutate(incomeRating = as.character(incomeRating)) %>%
  mutate(incomeRating=as.factor(str_replace(incomeRating, 'NA', 'UNK')))
  ```
