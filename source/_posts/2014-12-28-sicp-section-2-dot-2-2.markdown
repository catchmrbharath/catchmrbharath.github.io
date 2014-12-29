---
layout: post
title: "SICP: Section 2.2.2"
date: 2014-12-28 17:52:13 +0530
comments: true
categories: [SICP]
---

The sections introduces us to trees using pairs as the underlying structure.

###Section example
``` scheme
(define (count-leaves x)
  (cond ((null? x) 0)
        ((not (pair? x)) 1)
        (else (+ (count-leaves (car x))
                 (count-leaves (cdr x))))))

(define x (cons (list 1 2) (list 3 4)))

(count-leaves x)
(count-leaves (list x x))
```

Each exercise of SICP makes me think more about recursion. The following exercise made me
think more about how to model recursion and what the returns are to be when recursing multiple
layers inside a tree.
### Exercise 2.27
``` scheme
(define (deep-reverse items)
  (define (deep-reverse-iter items ans)
    (cond ((null? items) ans)
          ((not (pair? items)) items)
          (else (deep-reverse-iter (cdr items)
                                   (cons (deep-reverse-iter (car items) nil)
                                         ans)))))
  (deep-reverse-iter items nil))
```

### Exercise 2.28
``` scheme
;;Exercise 2.28
(define (fringe items)
  (define (fringe-iter list1 ans)
    (cond ((null? list1) ans)
          ((pair? list1) (append (fringe-iter (car list1) nil) (fringe-iter (cdr list1) nil)))
          (else (list list1))))
  (fringe-iter items nil)
  )
```

###Exercise 2.30

``` scheme
;;Exercise 2.30
(define (square-tree tree)
  (cond ((null? tree) nil)
        ((not (pair? tree)) (square tree))
        (else (cons (square-tree (car tree))
                    (square-tree (cdr tree))))))

(define (square-tree tree)
  (map (lambda (sub-tree)
         (if (pair? sub-tree)
           (square-tree sub-tree)
           (square sub-tree))) 
       tree))

(square-tree
  (list 1
        (list 2 (list 3 4) 5)
        (list 6 7)))
```

###Exercise 2.31

``` scheme
(define (tree-map proc tree)
  (map (lambda (sub-tree)
         (if (pair? sub-tree)
           (tree-map proc sub-tree)
           (proc sub-tree)))
       tree))

(define (square-tree tree) (tree-map square tree))
```

Exercise 2.32 could have been written better if currying was available. I am not sure whether scheme supports currying functions, and hence the
regular lambda expression.

### Exercise 2.32
``` scheme
;;Exercise 2.32
(define (subsets s)
  (if (null? s)
    (list nil)
    (let ((rest (subsets (cdr s))))
      (append rest (map (lambda (x) (cons (car s) x)) rest)))))
(subsets (list 1 2 3))
```




