# Exercise 8.3.8
## Question
For the <span style="font-family:Courier">index()</span> program in Chapter 7, complete the test sets for the following coverage criteria by filling in the “don’t care” values. Make sure to ensure reachability. Then derive the expected output. Download the program, compile it, and run it with your resulting test cases to verify correct outputs.

a) Predicate Coverage (PC)

b) Clause Coverage (CC)

c) Combinatorial Coverage (CoC)

d) Correlated Active Clause Coverage (CACC)

## Answer
The test cases for this program are simple:
- `subject = "hello", pattern = "ell"`
- `subject = "hello", pattern = "abc"`
- `subject = "", pattern = "e"`
- `subject = "e", pattern = ""`

Surely these test cases ensure reachability.

There are loops hence, it's hard to determine values of predicates and clauses.

Therefore, a), b), c), d) have same test sets.

```Java
import org.junit.Test;

import static org.junit.Assert.assertEquals;

public class Test_PatternIndex {
    @Test
    public void test_patterIndex_found()
    {
        assertEquals(PatternIndex.patternIndex("hello", "ell"), 1);
    }
    @Test
    public void test_patternIndex_emptyString()
    {
        assertEquals(PatternIndex.patternIndex("hello", ""), -1); // Only this fails
        assertEquals(PatternIndex.patternIndex("", "ell"), -1);

    }
    @Test
    public void test_patternIndex_notFound()
    {
        assertEquals(PatternIndex.patternIndex("hello", "hellooo"), -1);
    }
}
```