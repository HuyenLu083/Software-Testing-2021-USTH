# Exercise 4.1
## Question
Submit printouts of all tests, your final version of Calc, and a screenshot showing that all tests pass.

### Calc.java
```Java
package com.company;

public class Calc {
    static public int add(int a, int b) {
        return a + b;
    }

    static public int minus(int a, int b) {
        return a - b;
    }

    static public int multiply(int a, int b) {
        return a * b;
    }

    static public double divide (int a, int b)
    {
        return (float) a/b;
    }
}
```
## Answer
### TestCalc.java
```Java
package com.company;

import org.junit.Test;
import static org.junit.Assert.*;

public class TestCalc {
    Calc calc = new Calc();
    private int a = 8;
    private int b = 2;

    @Test
    public void testAdd() {
        assertEquals(calc.add(a, b), 10);
    }

    @Test
    public void testMinus() {
        assertEquals(calc.minus(a, b), 6);
    }

    @Test
    public void testMultiply() {
        assertEquals(calc.multiply(a, b), 16);
    }

    @Test
    public void testDivide() {
        assertEquals(calc.divide(a, b), 4, 0);
    }
}
```

### Proof
![title](Ex-4.1.png)