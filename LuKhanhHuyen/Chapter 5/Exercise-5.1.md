# Exercise 5.1
## Question
Suppose that coverage criterion C1 subsumes coverage criterion C2. Further suppose that test set T1 satisfies C1 on program P, and test set T2 satisfies C2, also on P.

## Answer
### (a) Does T1 necessarily satisfy C2?
Yes, because T1 satisfies C1 and C1 subsumes C2.

### (b) Does T2 necessarily satisfy C1?
No, because T2 only satisfies C2, which is smaller than C1.

### (c) If P contains a fault, and T2 reveals the fault, T1 does not necessarily also reveal the fault.
There is no requirement that test set T2 be a subset of test set T1. So, it could happen that T2 contains that one test that reveals the fault, and T1 doesn't.
