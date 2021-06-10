# Exercise 7.4.4
## Question
Use the following methods <span style="font-family:Courier">trash()</span> and <span style="font-family:Courier">takeOut()</span>:
```Java
/* 1 */ public void trash (int x) 
/* 2 */ {
/* 3 */ int m, n; 
/* 4 */
/* 5 */     m = 0;
/* 6 */     if (x > 0)
/* 7 */     m = 4;
/* 8 */     if (x > 5)
/* 9 */         n = 3*m;
/* 10 */    else 
/* 11 */        n = 4*m; 
/* 13 */    int o = takeOut (m, n10
/* 14 */    System.out.println ("o is: " + o);
/* 15 */}
/* 16 */public int takeOut (int a, int b)
/* 17*/{
/* 18 */    int d, e;
/* 19 */
/* 20 */    d = 42*a;
/* 21*/    if (a > 0)
/* 22 */        e = 2*b+d;
/* 23 */    else
/* 24 */        e = b+d;
/* 25 */    return (e);
/* 26 */}
```

## Answer
### a) Give all call sites using the line numbers given.
* For variable `m`, lines are 3, 5, 7, 9, 11, 12
* For variable `n`, lines are 3, 9, 11, 12

### b) Give all pairs of last-defs and first-uses.
* For variable m, last def is in line 7, first use is in line 9
* For variable n, last def is in line 11, first use is in line 21

### c) Provide test inputs that satisfy all-coupling-uses.
* x = 1
* x = 6
* x = 0