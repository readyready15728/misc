# Racket Notes
## Notes on the metastasized Scheme implementation

* Every Racket file needs a language declaration at the top.
* Exact decimals (for currency) e.g. can be represented like so: `#e.3`. See
  also: https://xn--w5d.cc/2020/11/24/racket-decimal.html
* `sort` has to be given the sorting function in every instance.
* `raco pkg install sicp` gave me the SICP language pack.
* `equal?` is used for most non-numeric equality comparisons. `=` does numeric
  equality comparisons with most reasonable semantics. `eq?` only does object
  reference equality.  
