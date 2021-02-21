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
* `for*` can be used for nested loops.
* Here's how to do a tail call-optimized `factorial`:

  ```racket
  (define (factorial n)
    (define (helper n acc)
      (if (= n 0)
          acc
          (helper (sub1 n) (* n acc))))
    (helper n 1))
  ```
* Here's the same thing, but memoized:

  ```racket
  (define (factorial)
    (let ([h (make-hash)])
      (define (factorial n)
        (cond
          [(= n 0) 1]
          [(hash-has-key? h n) (hash-ref h n)]
          [else
           (define (helper n acc)
             (if (= n 0)
                 acc
                 (helper (sub1 n) (* n acc))))
           (helper n 1)]))
      factorial))
  ```

* A memoized Fibonacci function:

  ```racket
  (define F
    (let ([f (make-hash)])
      (define (fib n)
        (cond
          [(<= n 1) n]
          [else
           (let ([fn (+ (fib (- n 1)) (fib (- n 2)))])
             (hash-set! f n fn)
             fn)]))
      fib))
  ```
