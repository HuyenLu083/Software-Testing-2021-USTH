# Exercise 8.3.5
## Question
Answer the following questions for the method <span style="font-family:Courier">checkIt()</span> below:
```java
   public static void checkIt (boolean a, boolean b, boolean c)
   {  
      if (a && (b || c))
      {
         System.out.println ("P is true");
      }
      else
      {
         System.out.println ("P isn't true");
      }
   }
```

(a) Transform <span style="font-family:Courier">checkIt()</span> to <span style="font-family:Courier">checkItExpand()</span>, a method where each if statement tests exactly one boolean variable. Instrument <span style="font-family:Courier">checkItExpand()</span> to record which edges are traversed. (“print” statements are fine for this.)

(b) Derive a GACC test set T1 for <span style="font-family:Courier">checkIt()</span>. Derive an EdgeCoverage test set T2 for <span style="font-family:Courier">checkItExpand()</span>. Build T2 so that it does not satisfy GACC on the predicate in <span style="font-family:Courier">checkIt()</span>.

(c) Run both T1 and T2 on both <span style="font-family:Courier">checkIt()</span> and <span style="font-family:Courier">checkItExpand()</span>.

## Answer
### (a)
**<span style="font-family:Courier">checkItExpand()</span>**

```java
public class CheckItExpand
{
  public static boolean checkItExpand(boolean a, boolean b, boolean c)
    {
        boolean ans = Boolean.parseBoolean(null);
        // Node 1
        if (a) // Node 2
        {
            if (b) ans = true; // Node 3
            else ans = false; // Node 4

            if (c) ans = true; // Node 5
            else ans = false; // Node 6
        } // Node 7
        else ans = false;
        return ans;
    }

  public static void main(String[] args) {
    boolean []inArr = new boolean [argv.length];
    if (argv.length != 3)
    {
       System.out.println ("Usage: java checkItExpand v1 v2 v3");
       return;
    }

    for (int i = 0; i< argv.length; i++)
    {
       inArr [i] = Boolean.parseBoolean(argv[i]);
    }

    checkItExpand (inArr[0], inArr[1], inArr[2]);
  }
}
```

### (b)
**For `CheckIt.java`**

Test set:
  - Test case 1: a = true, b = true, c = true. Expect: true
  - Test case 2: a = false, b = true, c = true. Expect: false
  - Test case 3: a = true, b = true, c = false. Expect: true
  - Test case 4: a = false, b = true, c = false. Expect: false
  - Test case 5: a = true, b = false, c = true. Expect: true
  - Test case 6: a = false, b = false, c = true. Expect: false

**For `CheckItExpand.java`**

- TR Edge:
[1,7]
[1,2,3]
[1,2,4,5]
[1,2,4,6]

* Test set:
  - Test case 1: a = false. Expect: false
  - Test case 2: a = true, b = true. Expect: true
  - Test case 3: a = true, b = false, c = true. Expect: true
  - Test case 4: a = true, b = false, c = false. Expect: false

### c)
### Test_CheckIt.java

```Java
import org.junit.Test;
import static org.junit.Assert.*;

public class Test_CheckIt {
    public static boolean checkIt (boolean a, boolean b, boolean c)
    {
        if (a && (b || c))
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    @Test
    public void test_checkIt()
    {
        assertTrue(checkIt(true, true, true));
        assertFalse(checkIt(false, true, true));
        assertTrue(checkIt(true, true, false));
        assertFalse(checkIt(false, true, false));
        assertTrue(checkIt(true, false, true));
        assertFalse(checkIt(false, false, true));
    }
}
```

### Test_CheckItExpand.java

```Java
import org.junit.Test;
import static org.junit.Assert.*;

public class Test_CheckItExpand {
    public static boolean checkItExpand(boolean a, boolean b, boolean c)
    {
        boolean ans = Boolean.parseBoolean(null);
        if (a)
        {
            if (b) ans = true;
            else
            {
                if (c) ans = true;
                else ans = false;
            }
        }
        else ans = false;
        return ans;
    }

    @Test
    public void test_checkItExpand()
    {
        assertFalse(checkItExpand(false, Boolean.parseBoolean(null), Boolean.parseBoolean(null)));
        assertTrue(checkItExpand(true, true, Boolean.parseBoolean(null)));
        assertTrue(checkItExpand(true, false, true));
        assertFalse(checkItExpand(true, false, false));
    }
}
```