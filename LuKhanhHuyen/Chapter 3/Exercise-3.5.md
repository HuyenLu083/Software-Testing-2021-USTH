# Exercise 3.5
## Question
Find the flaw and describe it in terms of the RIPR model. 
```Java
@Test
public void testSort()
{
  names.add("Laura");
  names.add("Han");
  names.add("Alex");
  names.add("Ashley");
  names.sort();
  assertTrue("Sort method", names.getFirst().equals ("Alex"));
}
```

## Answer
This assertion only check for the first element.

RIRP model:
* Reachable: if the fault is in the first element then it is reached, but if for other elements, then it is not reached.
* Infection: yes
* Propagation: no, the whole list can be incorrect but first element can still be correct.
* Reveal: no, the test assertion cannot reveal the fault.