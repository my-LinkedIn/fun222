# Solution to Fun Math #222

https://www.linkedin.com/feed/update/urn:li:activity:7205010763072036864?utm_source=share&utm_medium=member_desktop

## Source code

```racket
#lang racket

(require math)

; Function to split a number into its digits
(define (digits n)
  (if (zero? n)
      '(0)
      (reverse (let loop ((n n) (acc '()))
                 (if (zero? n)
                     acc
                     (loop (quotient n 10) (cons (modulo n 10) acc)))))))

; Function to combine a list of digits into a number
(define (undigits lst)
  (foldl (lambda (d acc) (+ (* 10 acc) d)) 0 lst))

; Generate the list of numbers and filter them
(define xs
  (filter (lambda (n)
            (= (undigits (sort (digits n) <)) 123456789))
          (range 1000001520 10000000000 2520)))

; Check if xs is empty and handle it
(if (null? xs)
    (displayln "No numbers satisfy the condition.")
    (begin
      (displayln (list (cadr (reverse xs))
                       (car (reverse xs))))
      (void)))
```

## Output

```text
(9876134520 9876351240)
```

## Reference

[Racket Language](https://racket-lang.org/)
