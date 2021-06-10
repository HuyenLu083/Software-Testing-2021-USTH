# Exercise 6.2-3

## Question
Write down all 16 tests to satisfy Multiple Base Choice coverage (MBCC) for the second categorization of `triang()`’s inputs in Table 6.2. Use the values in Table 6.3.

## Answer
The two base tests are (2, 2, 2) and (1, 2, 2), and the following additional tests would be needed:
* For base test (2, 2, 2):
  
    (2, 2, 2)

    (0, 2, 2) (-1, 2, ,2)

    (2, 1, 2) (2, 0, 2)	(2, -1, 2)

    (2, 2, 1) (2, 2, 0)	(2, 2, -1)

* For base test (1, 2, 2):
  
    (1, 2, 2)

    (0, 2, 2) (−1, 2, 2)

    (1, 1, 2) (1, 0, 2)	(1, −1, 2)

    (1, 2, 1) (1, 2, 0)	(1, 2, −1)
