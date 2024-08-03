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
* `install.packages` didn't work for DMwR. Here's what did:

  ```r
  library(devtools)
  remotes::install_github('cran/DMwR')
  ```
  
  (I had equal success installing ggtheme in a similar fashion.)
* `attrition` is no longer in `rsample`. To gain access to `attrition`,
  install `modeldata`, then do:

  ```r
  library(modeldata)
  data(attrition, package='modeldata')
  ```
* `verboseIter=TRUE` as an argument to `trainControl` will enable progress
  tracking during runs of `train`.
* Tidyverse packages include `glimpse()` which gives a quick rundown of a
tibble (or presumably a regular dataframe too).
* I still don't fully understand, but refer to page 11 of `R for Data
Science`, 2nd Edition (O'Reilly) for how to get single vs. multiple
estimated lines for `geom_smooth()` being used with `color` or the like.
* `geom_density()` with `color`, `fill` and `alpha` can be very nice.
* `geom_bar()` with `position='fill'` can be used to show relative frequency
well.
* Consider using `facet_wrap()` and maybe even `facet_grid()`.
* "`count()` lets you quickly count the unique values of one or more
variables: `df %>% count(a, b)` is roughly equivalent to
`df %>% group_by(a, b) %>% summarise(n = n())`.".
* Consider using `.groups='keep'` with `summarize()`. (I refuse to use the
limey spelling.)
* Better to use a common prefix than a common suffix in variable naming.
* Configure RStudio never to use `.RData`.
* Concerning the difference between `unique()` and `distinct()`: https://stackoverflow.com/questions/45198738/difference-between-distinct-vs-unique
* The ColorBrewer scales have been hand-tuned to be effective with people
having various types of color blindness and there are online color blindness
simulators etc. to test things out.
* Use `is.na()` and `near()` as needed.
* `flights |> filter(month == 1, day == 1) |> arrange(desc(is.na(dep_time)), dep_time)`
makes rows with `dep_time` equal to NA appear first.
* `if_else()` and the more advanced `case_when()` are in dplyr and they rock.
* `n_distinct()` is also quite useful.
* `pmin()` and `pmax()` return parallel extrema among two or more vectors.
* `forcats::fct()` as opposed to `factor()` won't silently turn values not
given in `levels` to `NA`s.
* `help(package='nycflights13')`.
* `flights |> ggplot(aes(x=carrier, fill=origin)) + geom_bar(position=position_dodge(preserve='single'))`.
* `flights |> ggplot(aes(x=carrier)) + geom_bar() + facet_wrap(~origin, ncol=1)`.
* `ncol=1` is especially important for the last one because not doing so
results in a very crowded x-axis.
* `,` can be used instead of `&` with `filter()`.
* `libR.so` needs to be available for RStudio to run. This can be made
available during compiliation from source. (I did so with
`./configure --enable-R-shlib --enable-BLAS-shlib --enable-memory-profiling --with-blas --with-lapack`.)
* The enhanced R shell radian also requires `libR.so`.
* `View()` works outside of RStudio but it uses an ugly Xaw interface. Oh
well. Note that `print()` has parameters `n` (rows) and `width` (columns) and
both can be supplied with `Inf`.
* `flights |> select(year, month, day, hour, minute, time_hour, everything())`.
* `flights %>% select(starts_with("a"))`.
* `flights %>% select(ends_with("delay"))`.
* `flights %>% select(contains("time"))`.
* `named_dests %>% top_n(n = 10, wt = num_flights)`.
*
  ```r
  flights |>
  inner_join(planes, by=c('tailnum')) |>
  select(carrier, distance, seats) |>
  mutate(available_seat_miles=distance * seats) |>
  group_by(carrier) |>
  summarize(available_seat_miles=sum(available_seat_miles)) |>
  arrange(desc(available_seat_miles))
  ```
* `guat_dem |> pivot_longer(names_to='year', values_to='democracy_score', cols=-country, names_transform=list(year=as.integer))`.
* `life_expectancy |> pivot_longer(names_to='year', values_to='life_expectancy', cols=-country) |> mutate(year=as.integer(year))`.
* `sample_n()`.
* `skim()` from `skimr` is really very good!
* `geom_jitter()` can be used to prevent overplotting.
* Consider using `boundary` with `geom_histogram()`.
* `options(pillar.sigfig = n)` sets precision of tibble printouts.
* A `tsibble` will retain its key even after a `group_by()` operation but will
lose its initial key when `summarize()` is carried out, which will then be
replaced with another key reflected by the `group_by()` operation.
