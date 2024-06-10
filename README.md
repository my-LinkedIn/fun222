# Proof/Solution to Fun Math #222

## D language

My usual language of choice...

### Source code

```d
import std.stdio;
import std.string;
import std.conv;
import std.range;
import std.algorithm;

/*
 1) LCM of the digits 1 through 9 is 2_520
 2) Lower bound (smallest ten-digit multiple of 2_520) is 1_000_001_520
 3) Generate all the ten-digit multiples of 2520
 4) Filter out number Pandigital and Divisible by 1 through 9
*/

bool isPandigitalAndDivisibleBy1Through9(long number) {
    foreach (i; 1 .. 10) {
        if (number % i != 0) {
            return false;
        }
    }
    return text(number.text.array.sort) == "0123456789";
}

void main() {
    auto seq10digits = iota(1_000_001_520, 10_000_000_000, 2_520)
                            .filter!isPandigitalAndDivisibleBy1Through9
                            .array;

    writeln("Second-to-last Element of the Sequence: ", seq10digits[$ - 2]);
    writeln("Last Element of the Sequence: ", seq10digits[$-1]);
}

```

### Output

```text
Second-to-last Element of the Sequence: 9876134520
Last Element of the Sequence: 9876351240
```

## Racket language [Bonus]

Trying other paradigms is tempting... a Taste of [Lisp](https://en.wikipedia.org/wiki/Lisp_(programming_language)) feeling this time, Go for it! 🏃‍♂️🏃‍♂️🏃‍♂️

### Source code

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

### Output

```text
(9876134520 9876351240)
```

## Reference

  - [Fun Math #222](https://www.linkedin.com/feed/update/urn:li:activity:7205010763072036864?utm_source=share&utm_medium=member_desktop)
  - [Dlang](https://dlang.org/)
  - [Racket Wikipedia entry](https://en.wikipedia.org/wiki/Racket_(programming_language))
  - [Racket Language website](https://racket-lang.org/)
  - [11460 terms pandigital numbers satisfying the property](https://oeis.org/A187565/b187565.txt)
