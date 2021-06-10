# Exercise 1.7
## Question
Consider the following three example classes. These are OO faults taken from Joshua Bloch’s Effective Java, Second Edition. Answer the following questions about each.

## Answer
## Vehicle, Truck
### a) Explain what is wrong with the given code. Describe the fault precisely by proposing a modification to the code.

The method clone() inside class Truck cannot use the clone() method of class Vehicle. One of possible modification is:
```Java
public class Vehicle implements Cloneable
{
    private int x;

    public Vehicle(int y) { x = y;}

    @Override public Object clone() {
        Object result = new Vehicle(this.x);
        // Location "A"
        return result;
    }
    @Override public boolean equals (Object o) {
        if (!(o instanceof Vehicle)) return false;
        Vehicle v = (Vehicle) o;
        return v.x == this.x;
    }
}
```
```Java
public class Truck extends Vehicle {
    private int y;
    public Truck(int z) {
        super(z);
        y = z;
    }
    @Override
    public Object clone() {
        Object result = new Vehicle(this.y);
        return result;
    }
    @Override
    public boolean equals(Object o) {
        if (!(o instanceof Truck)) return false;
        Truck t = (Truck) o;
        return super.equals(t) && t.y == this.y;
    }
    // other methods omitted
}
```

### b) If possible, give a test case that does not execute the fault. If not, briefly explain why not.
A test case that does not execute the fault in simply does not call the method Truck.equals()

### c) If possible, give a test case that executes the fault, but does notresult in an error state. If not, briefly explain why not.
A test case that executes the fault in but does not create result in an error state does not create an instance of a subclass.

## BigDecimalTest
### a) Explain what is wrong with the given code. Describe the fault precisely by proposing a modification to the code.
The fault is the inconsistency between methods compareTo() and equals(). One of possible modification is:
```Java
import static org.junit.Assert.*;
import org.junit.*;
import java.util.*;
import java.math.*;

public class BigDecimalTest {
  private BigDecimal x;
  private BigDecimal y;

  Set <BigDecimal> tree;
  Set <BigDecimal> hash;

  @Before public void setUp() {
     x = new BigDecimal("1.0");
     y = new BigDecimal("1.00");
     // Fact:  !x.equals(y), but x.compareTo(y) == 0

     tree = new TreeSet <BigDecimal> ();
     hash = new HashSet <BigDecimal> ();
  }
}  
```

### b) If possible, give a test case that does not execute the fault. If not, briefly explain why not.
No test case that can not execute the fault.

### c) If possible, give a test case that executes the fault, but does notresult in an error state. If not, briefly explain why not.
A test case that executes the fault but does not create result in an error state is 1.00 and 2.00.