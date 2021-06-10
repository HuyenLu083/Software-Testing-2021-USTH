# Exercise 1.5
## Question
Below are four faulty programs. Each includes test inputs that result in failure. Answer the following questions about each program.

## Answer
## findLast
```Java
public static int findLast (int[] x, int y)
   {
      for (int i = x.length-1; i > 0; i--)
      {
         if (x[i] == y)
         {
            return i;
         }
      }
      return -1;
   }
```

## lastZero
```Java
public static int lastZero (int[] x)
   {
      for (int i = 0; i < x.length; i++)
      {
         if (x[i] == 0)
         {
            return i;
         }
      }
      return -1;
   }
```

## countPositive
```Java
public static int countPositive (int[] x)
   {
      int count = 0;
      for (int i=0; i < x.length; i++)
      {
         if (x[i] >= 0)
         {
            count++;
         }
      }
      return count;
   }
```

## oddOrPos
```Java
public static int oddOrPos (int[] x)
   {  
      int count = 0;
      for (int i = 0; i < x.length; i++)
      {
         if (x[i]%2 == 1 || x[i] > 0)
         {
            count++;
         }
      }
      return count;
   }
```

### a) Explain what is wrong with the given code. Describe the fault precisely by proposing a modification to the code.
* findLast: the condition for the loop is wrong
```Java
for (int i=x.length-1; i >= 0; i--)
```

* countPositive: the condition in the if statement is wrong
```Java
if (x[i] > 0)
```

### b) If possible, give a test case that does not execute the fault. If not, briefly explain why not.
* findLast: `int[] x = {2, 3, 5}` and `y = 2`
* lastZero: `int[] x = {0, 1, 2}`
* countPositive: `int[] x = {-4, 2, 3, -8}`
* oddOrPos: `int[] x = {1, 2, 3}`

### c) If possible, give a test case that executes the fault, but does not result in an error state. If not, briefly explain why not.
* findLast: `int[] x = {2, 2, 5}` and `y = 2`
* lastZero: `int[] x = {0}`
* countPositive: Not Possible
* oddOrPos: `int[] x = {1, 2, 3}`