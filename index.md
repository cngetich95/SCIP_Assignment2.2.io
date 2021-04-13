## Welcome to GitHub Pages

;; SICP 2.2
;; **Question**
;; Exercise 2.2.  Consider the problem of representing line segments
;; in a plane. Each segment is represented as a pair of points: a
;; starting point and an ending point. Define a constructor
;; make-segment and selectors start-segment and end-segment that
;; define the representation of segments in terms of
;; points. Furthermore, a point can be represented as a pair of
;; numbers: the x coordinate and the y coordinate. Accordingly,
;; specify a constructor make-point and selectors x-point and y-point
;; that define this representation. Finally, using your selectors and
;; constructors, define a procedure midpoint-segment that takes a line
;; segment as argument and returns its midpoint (the point whose
;; coordinates are the average of the coordinates of the
;; endpoints). To try your procedures, you'll need a way to print
;; points:

;; (define (print-point p)
;;   (newline)
;;   (display "(")
;;   (display (x-point p))
;;   (display ",")
;;   (display (y-point p))
;;   (display ")"))

;; **Solution** ------------------------------------------------------------

(define make-segment cons)
(define start-segment car)
(define end-segment cdr)

(define make-point cons)
(define x-point car)
(define y-point cdr)

(define (sum . l) (if (zero? (length l)) 0 (+ (car l) (apply sum (cdr l)))))
(define (average . l) (/ (apply + l) (length l)))

(define point->coordinate-accessors (list x-point y-point))
(define (midpoint seg)
  (apply make-point (map (lambda (point->coordinate)
                           (average (point->coordinate (start-segment seg))
                                    (point->coordinate (end-segment seg))))
                         point->coordinate-accessors)))

(define (print-point p)
  (newline)
  (display "(")
  (display (x-point p))
  (display ",")
  (display (y-point p))
  (display ")"))

(define seg-1 (make-segment (make-point 3 4)
                            (make-point 8 10)))
(print-point (midpoint seg-1))
