# Exercise 6.4-2
## Question
It is possible to modify an <span style="font-family:Courier">ArrayList</span> without using the <span style="font family:Courier">remove()</span> method and yet have a subsequent call to <span style="font-family:Courier">remove()</span> fail to throw <span style="font-family:Courier">ConcurrentModificationException</span>. Develop a (failing) JUnit test that exhibits this behavior.

## Answer
### failingTest
```Java
import static org.junit.Assert.*;
import org.junit.*;
import java.util.*;

public class failingTest {
    private List<String> list;
    private Iterator<String> itr;

    @Test (expected=ConcurrentModificationException.class)
    public void testRemove() {
        list = new ArrayList<String>();
        list.add ("atk");
        list.add ("def");
        itr = list.iterator();
        itr.next();
        list.add("something");
        itr.remove();
    }
}
```