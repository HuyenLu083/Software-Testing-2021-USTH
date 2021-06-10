# Exercise 8.3.9
## Question
For the <span style="font-family:Courier">Quadratic</span> program in Chapter 7, complete the test sets
for the following coverage criteria by filling in the “don’t care”
values. Make sure to ensure reachability. Then derive the expected
output. Download the program, compile it, and run it with your
resulting test cases to verify correct outputs.

(a) Predicate Coverage (PC)

(b) Clause Coverage (CC)

(c) Combinatorial Coverage (CoC)

(d) Correlated Active Clause Coverage (CACC)

## Answer
### Quadratic class
```Java
// Program to compute the quadratic root for two numbers
import java.lang.Math;

public class Quadratic
{
    public static double Root1, Root2;
    // Finds the quadratic root, A must be non-zero
    public static boolean Root (int A, int B, int C)
    {
        double D;
        boolean Result;
        D = (double)(B*B) - (double)(4.0*A*C);
        if (D < 0.0)
        {
            Result = false;
            return (Result);
        }
        Root1 = (double) ((-B + Math.sqrt(D)) / (2.0*A));
        Root2 = (double) ((-B - Math.sqrt(D)) / (2.0*A));
        Result = true;
        return (Result);
    } // End method Root

    public static void main (String[] argv)
    {
        int X, Y, Z;
        boolean ok;
        if (argv.length == 3)
        {
            try
            {  // The book has a typo in this example,
                // argv[] must start at 0, not 1.
                // This version has been corrected.
                X = Integer.parseInt (argv[0]);
                Y = Integer.parseInt (argv[1]);
                Z = Integer.parseInt (argv[2]);
            }
            catch (NumberFormatException e)
            {
                System.out.println ("Inputs not three integers, using 8, 10, -33.");
                X = 8;
                Y = 10;
                Z = -33;
            }
        }
        else
        {
            System.out.println ("Inputs not three integers, using 8, 10, -33.");
            X = 8;
            Y = 10;
            Z = -33;
        }
        ok = Root (X, Y, Z);
        if (ok)
            System.out.println
                    ("Quadratic: Root 1 = " + Root1 + ", Root 2 = " + Root2);
        else
            System.out.println ("No solution.");
    }
} // End class Quadratic
```

There is only one predicate with one clause.
Therefore, a), b), c), d) have same test sets.

Test set:
- Test case 1: A = 1, B = -8, C = 15
- Test case 2: A = 1, B = -4, C = 4
- Test case 3: A = 1, B = -1, C = 1

### Test_Quadratic class
```Java
import org.junit.Test;
import static org.junit.Assert.*;

public class Test_Quadratic {
    @Test
    public void test_root()
    {
        assertTrue(Quadratic.Root(1, -8, 15));
        assertTrue(Quadratic.Root(1, -4, 4));
        assertFalse(Quadratic.Root(1, -1, 1));
    }
}
```