# Exercise 9.2.1

## Question
Provide reachability conditions, infection conditions, propagation conditions, and test case values to kill mutants 2, 4, 5, and 6 in Figure 9.1.

```Java
int min(int A, int B)
{
  int minVal;
  minVal = A;
  if (B < A)
  {
    minVal = B;
  }
  return minVal;
}
```

## Answer
### Mutant 2
- Reachability condition: The statement will be reached.  
- Infection condition: The test will infect if the predicate gives a different result.  
- Propagation condition: The infection will force another path, which will propagate.

```Java
int min(int A, int B)
{
  int minVal;
  minVal = A;
  if (B > A)
  {
    minVal = B;
  }
  return minVal;
}
```

Test case: A = 5, B = 6

### Mutant 4
- Reachability condition: Reached if ( B < A ) is true.  
- Infection condition: Bomb() will infect.
- Propagation condition: True, Bomb() will propagate.

```Java
int min(int A, int B)
{
  int minVal;
  minVal = A;
  if (B < A)
  {
    minVal = B;
    Bomb();
  }
  return minVal;
}
```

Invalid Mutant.

Test case: A = 6, B = 5

### Mutant 5
- Reachability condition: Reached if ( B < A ) is true. 
- Infection condition: True if A != B.
- Propagation condition: minVal got another value, then it will propagate.

```Java
int min(int A, int B)
{
  int minVal;
  minVal = A;
  if (B < A)
  {
    minVal = B;
    minVal = A;
  }
  return minVal;
}
```

Test case: A = 6, B = 5

### Mutant 6
- Reachability condition: Reached if ( B < A ) is true. 
- Infection condition: if B = 0.
- Propagation condition: fail -> propagate.

```Java
int min(int A, int B)
{
  int minVal;
  minVal = A;
  if (B < A)
  {
    minVal = B;
    minVal = failOnZero(B);
  }
  return minVal;
}
```

Test case: A = 5, B = 0