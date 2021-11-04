# Iterative Fibonacci in Scheme
## The one in SICP made less sense

I seem to remember adapting the one from Rosetta Code:

```scheme
(define (fib-iter a b count)
  (if (= count 0)
    a
    (fib-iter b (+ a b) (- count 1))))

(define (fib n)
  (fib-iter 0 1 n))
```
