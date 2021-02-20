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
* `sudo raco pkg install -i <package name(s)>` is necessary for system-wide
  installation of Racket packages. (The default behavior is to install into
  `/root` when using `sudo`.)
* Example of partial function application in Racket: https://rosettacode.org/wiki/Partial_function_application#Racket
* The `let*` form can be used to reference values bound in other bindings.
* Note that `remainder` and `modulo` have different behavior.
* `empty` is an alias for `'()`.
* In the context of a `for` statement, a positive integer can create a stream,
  like so:

    ```racket
    (for ([i 5])
        (display i)
        (newline))
    ```
