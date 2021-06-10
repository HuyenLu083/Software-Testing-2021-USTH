# Exercise 6.1-2
## Question
A tester defined three characteristics based on the input parameter car: Where Made, Energy Source, and Size. The following partitionings for these characteristics have at least two mistakes. Correct them.
```
    +---------------------------------------+
    |             Where made                |
    +---------------+----------+------------+
    | North America | Europe   | Asia       |
    +---------------+----------+------------+
    |            Energy Source              |
    +---------------+----------+------------+
    | gas           | electric | hybrid     |
    +---------------+----------+------------+
    |               Size                    |
    +---------------+----------+------------+
    | 2-door        | 4-door   | hatch back |
    +---------------+----------+-------------
```
## Answer
### Problems:
* Where Made: Cars can be manufactured at other places than the 3 mentioned. The tester should include an "other" case.
* Energy Source: Hybrid overlaps gas and electric. The tester should remove hybrid.
* Size: A hatch-back car can have 2 or 4 doors. So the tester should split this into two distince characteristics: Number of doors and hatch-back.

### Correct:
There should be 4 characteristics:
* Where Made: North America, Europe, Asia, Other
* Energy Source: gas, electric
* Number of Doors: 2, 4
* Hatch-back: True, False