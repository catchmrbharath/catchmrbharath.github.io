---
layout: post
title: "SICP: Section 2.2.1"
date: 2014-12-28 16:46:08 +0530
comments: true
categories: [SICP]
---

Exercise 2.20 deals with functions that take arbitrary number of arguments. This is extremely
useful in the context of scheme because it allows you to use less brackets :).

###Exercise 2.20
``` scheme
(define (same-parity elem . xlist)
  (define (same-parity-iter res-list num-list)
    (if (null? num-list)
      res-list
      (if (= (remainder (+ elem (car num-list)) 2) 0)
        (same-parity-iter (cons (car num-list) res-list) (cdr num-list))
        (same-parity-iter res-list (cdr num-list)))))
  (reverse (same-parity-iter (list elem) xlist)))

```

I used `reverse` followed by the `same-parity-iter` because I did not want to use the inefficient
`append` function. 

```
(same-parity 1 2 3 4 5 6 7)
mcons 4 (mcons 3 (mcons 5 (mcons 7 '()'))))
```

The sections also introduces us to the `map` higher order function.

```
(define (map proc items)
  (if (null? items)
    nil
    (cons (proc (car items))
          (map proc (cdr items)))))
```

But why map? Quoting SICP

{% blockquote %}
The different between the two definitions is not that the computer is performing a different process (it isn't) but that we think about the process differently. In effect, `map` helps establish an abstraction barrier that isolates the implementation of procedures that transforms lists from the details of how the elements of the list are extracted and combined.

{% endblockquote %}

This is the most succint way to put across the need for abstractions. Abstractions are invented to help us think differently
and care about different things.

###Exercise 2.21
``` scheme
;;Exercise 2.21
;; without using map
(define (square x) (* x x))
(define (square-list items)
  (if (null? items)
    nil
    (cons (square (car items))
          (square-list (cdr items)))))

;;with using map
(define (square-list items)
  (map (lambda (x) (* x x))
       items))
```

###Exercise 2.22

``` scheme
;;Exercise 2.22
;; Iterative square list

(define (square-list items)
  (define (iter things answer)
    (if (null? things)
      answer
      (iter (cdr things)
            (cons (square (car things))
                  answer))))
  (iter items nil))
```

Interchanging the arguments of cons does not work as it will generate a list of lists instead of generating 
a single list.

###Exercise 2.23

``` scheme
;; Exercise 2.23

(define (for-each proc items)
  (cond ((null? items) #t)
        (else (proc (car items))
              (for-each proc (cdr items)))))

(for-each (lambda (x) (newline) (display x))
          (list 57 321 68))
```


