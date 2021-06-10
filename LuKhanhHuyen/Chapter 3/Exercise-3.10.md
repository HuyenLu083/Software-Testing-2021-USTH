# Exercise 3.10
## Question
Replace each occurrence of a set with a list in the JUnit theory <span style="font-family:Courier">removeThenAddDoesNotChangeSet</span>. Is the resulting theory valid or invalid? How many of the tests that pass the precondition also pass the postcondition? Explain.

## Answer
### ListTheoryTest.java
```Java
import org.junit.*;
import org.junit.runner.RunWith;
import static org.junit.Assert.*;
import static org.junit.Assume.*;

import org.junit.experimental.theories.DataPoint;
import org.junit.experimental.theories.DataPoints;
import org.junit.experimental.theories.Theories;
import org.junit.experimental.theories.Theory;

import java.util.*;

@RunWith (Theories.class)
public class ListTheoryTest
{
    @DataPoints
    public static String[] string = {"ant", "bat", "cat"};

    @DataPoints
    public static List[] lists = {
            Arrays.asList ("ant", "bat"),
            Arrays.asList ("bat", "cat", "dog", "elk"),
            Arrays.asList ("Snap", "Crackle", "Pop")
    };

    @Theory
    public void removeThenAddDoesNotChangeList
            (List<String> list, String string)
    {
        assumeTrue (list != null);
        assumeTrue (list.contains (string));
        List<String> copy = new ArrayList<String>(list);
        copy.remove (string);
        copy.add (string);
        assertEquals(list, copy);
    }
}
```

### SetTheoryTest.java
```Java
import org.junit.*;
import org.junit.runner.RunWith;
import static org.junit.Assert.*;
import static org.junit.Assume.*;

import org.junit.experimental.theories.DataPoint;
import org.junit.experimental.theories.DataPoints;
import org.junit.experimental.theories.Theories;
import org.junit.experimental.theories.Theory;

import java.util.*;

@RunWith (Theories.class)
public class SetTheoryTest
{
    @DataPoints
    public static String[] string = {"ant", "bat", "cat"};

    @DataPoints
    public static Set[] sets = {
            new HashSet (Arrays.asList ("ant", "bat")),
            new HashSet (Arrays.asList ("bat", "cat", "dog", "elk")),
            new HashSet (Arrays.asList ("Snap", "Crackle", "Pop"))
    };


    @Theory
    public void removeThenAddDoesNotChangeSet
            (Set<String> set, String string)
    {
        assumeTrue (set != null);      
        assumeTrue (set.contains (string));
        Set<String> copy = new HashSet<String>(set); 
        copy.remove (string);
        copy.add (string);
        assertTrue (set.equals (copy));     
    }
}
```

For ListTheoryTest, no test pass in contrast for SetTheoryTest, all test pass.

The reason why we get this result is the different in meaning of set and list. List can have duplicate element while set only distinct elements.