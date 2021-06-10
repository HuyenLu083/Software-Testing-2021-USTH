# Exercise 6.4-1

## Question
The restriction on interleaving <span style="font-family:Courier">next()</span> and <span style="font-family:Courier">remove()</span> calls is quite complex. The JUnit tests in <span style="font-family:Courier">IteratorTest.java</span> only devote onetest for this situation, which may not be enough. Refine the input domain model with one or more additional characteristics to probe this behavior, and implement these tests in JUnit.

## Answer
The following characteristics have been identified and are used to generate tests for the methods:
- C1: iterator has more values
- C2: iterator returns a non-null object reference
- C3: remove() is supported
- C4: remove() precondition is satisfied
- C5: collection in consistent state while iterator in use
- Each characteristic has a boolean partition

After that, the condition for the tests is set up.
```Java
import static org.junit.Assert.*;
import org.junit.*;
import java.util.*;

public class IteratorTest {
	
   private List<String> list;      
   private Iterator<String> itr;   

   @Before public void setUp()  
   {
      list = new ArrayList<String>();
      list.add ("cat");
      list.add ("dog");
      itr = list.iterator();
   }
```

### Tests for Iterator method next()
Since this is only for the next() method, C3 and C4 characteristics are not associated. Warning: in the second test case where C1 is removed, C2 is also not satisfied since the next value must be null. In the last test case where the iterator is changed while in use, C2 is not satisfied because there are inconsistencies.

```Java
    // Test 1 of next(): testNext_BaseCase(): C1-T, C2-T, C5-T
    @Test public void testNext_BaseCase()
    {
        assertEquals ("cat", itr.next());
    }

    // Test 2 of next(): testNext_C1(): C1-F, C2-F, C5-T
    @Test(expected=NoSuchElementException.class)
    public void testNext_C1()
    {
        itr.next(); itr.next();        // consume the cat and the dog
        itr.next();                    // now empty
    }

    // Test 3 of next(): testNext_C2(): C1-T, C2-F, C5-T
    @Test public void testNext_C2()
    {
        list = new ArrayList<String>();
        list.add (null);
        itr = list.iterator();
        assertNull (itr.next());
    }

    // Test 4 of next(): testNext_C5(): C1-T, C2-F, C5-F
    @Test(expected=ConcurrentModificationException.class)
    public void testNext_C5()
    {
        list.add ("elephant");
        itr.next();
    }
```

### Tests for Iterator method remove()
The remove() method is tested using the "Base Choice" criterion. All 5 characteristics above are associated with the remove() method and each characteristic is removed while keeping the other 4. Warning: in the second test case where C1 is False, C2 also has to be False because if the iterator does not have anymore value, the return value has to be null.
```Java
    // Test 1 of remove(): testRemove_BaseCase(): C1-T, C2-T, C3-T, C4-T, C5-T
    @Test public void testRemove_BaseCase()
    {
        itr.next();
        itr.remove();
        assertFalse (list.contains ("cat"));
    }

    // Test 2 of remove(): testRemove_C1(): C1-F, C2-F, C3-T, C4-T, C5-T
    @Test public void testRemove_C1()
    {
        itr.next(); itr.next();        // consume the cat and the dog
        itr.remove();                  // remove dog from list.
        assertFalse (list.contains ("dog"));
    }

    // Test 3 of remove(): testRemove_C2(): C1-T, C2-F, C3-T, C4-T, C5-T
    @Test public void testRemove_C2()
    {
        list.add (null);
        list.add ("elephant");
        itr = list.iterator();
        itr.next(); itr.next();        // consume the cat and the dog
        itr.next();        // consume null; iterator not empty
        itr.remove();      // remove null from list
        assertFalse (list.contains (null));
    }

    // Test 4 of remove(): testRemove_C3(): C1-T, C2-T, C3-F, C4-T, C5-T
    @Test(expected=UnsupportedOperationException.class)
    public void testRemove_C3()
    {
        list = Collections.unmodifiableList (list);
        itr = list.iterator();
        itr.next();   // consume first element to make C4 true
        itr.remove();
    }

    // Test 5 of remove(): testRemove_C4(): C1-T, C2-T, C3-T, C4-F, C5-T
    @Test (expected=IllegalStateException.class)
    public void testRemove_C4()
    {
        itr.remove();
    }


    // Test 6 of next(): testRemove_C5(): C1-T, C2-T, C3-T, C4-T, C5-F
    @Test (expected=ConcurrentModificationException.class)
    public void testRemove_C5()
    {
        itr.next();
        list.add ("elephant");
        itr.remove();
    }
```
