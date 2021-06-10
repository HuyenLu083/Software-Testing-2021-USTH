# Exercise 3.3
## Question
Develop JUnit tests for the BoundedQueue class. A compilable version is available on the book website in the file BoundedQueue.java. Make sure your tests check every method, but we will not evaluate the quality of your test designs and do not expect you to satisfy any test criteria. Turn in a printout of your JUnit tests and either a printout or a screen shot showing the results of each test.

### BoundedQueue()
```Java
public class BoundedQueue
{
    // Overview:  a BoundedQueue is a mutable, bounded FIFO data structure
    // of fixed size , with size being set in the constructor
    // A typical Queue is [], [o1], or [o1, o2], where neither o1 nor o2
    // are ever null.  Older elements are listed before newer ones.

    private final Object[] elements;
    private int size, front, back;
    private final int capacity;

    public BoundedQueue (int capacity)
    {
        if (capacity < 0)
            throw new IllegalArgumentException ("BoundedQueue.constructor");
        this.capacity = capacity;
        elements = new Object [capacity];
        size  = 0; front = 0; back  = 0;
    }

    public void enQueue (Object o)
            throws NullPointerException, IllegalStateException
    {  // Modifies: this
        // Effects:   If argument is null throw NullPointerException
        // else if this is full, throw IllegalStateException,
        // else make o the newest element of this
        if (o == null)
            throw new NullPointerException ("BoundedQueue.enQueue");
        else if (size == capacity)
            throw new IllegalStateException ("BoundedQueue.enQueue");
        else
        {
            size++;
            elements [back] = o;
            back = (back+1) % capacity;
        }
    }

    public Object deQueue () throws IllegalStateException
    {  // Modifies: this
        // Effects:   If queue is empty, throw IllegalStateException,
        // else remove and return oldest element of this

        if (size == 0)
            throw new IllegalStateException ("BoundedQueue.deQueue");
        else
        {
            size--;
            Object o = elements [ (front % capacity) ];
            elements [front] = null;
            front = (front+1) % capacity;
            return o;
        }
    }

    public boolean isEmpty()
    {
        return (size == 0);
    }
    public boolean isFull()
    {
        return (size == capacity);
    }

    public String toString()
    {
        String result = "[";
        for (int i = 0; i < size; i++)
        {
            result += elements[ (front + i) % capacity ] . toString();
            if (i < size -1) {
                result += ", ";
            }
        }
        result += "]";
        return result;
    }

}
```
## Answer
### TestBoundedQueue()
```Java
package com.company;

import org.junit.Test;
import static org.junit.Assert.*;

public class TestBoundedQueue {
    BoundedQueue queue = new BoundedQueue(3);

    @Test
    public void testEmptyQueue() {
        assertTrue(queue.isEmpty());
    }

    @Test
    public void testEnqueue() {
        String str = "Hello, I am Huyen";
        queue.enQueue(str);
        assertFalse(queue.isEmpty());
    }

    @Test
    public void testDequeue() {
        String str = "Hello, I am Huyen";
        queue.enQueue(str);
        assertEquals(str, queue.deQueue());
    }

    @Test
    public void testFullQueue() {
        String a, b, c;
        a = "Lu";
        b = "Khanh";
        c = "Huyen";

        queue.enQueue(a);
        queue.enQueue(b);
        assertFalse(queue.isFull());

        queue.enQueue(c);
        assertTrue(queue.isFull());
    }

    @Test
    public void testToString() {
        String a, b, c;
        a = "Lu";
        b = "Khanh";
        c = "Huyen";

        queue.enQueue(a);
        queue.enQueue(b);
        queue.enQueue(c);

        assertEquals("[Lu, Khanh, Huyen]", queue.toString());
    }
}
```

## Proof
![title](Ex3-3.png)