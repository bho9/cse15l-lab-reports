# Lab Report 2 Week 4
---
## Code change 1:

![Image](/lab2week4ss/Figure3.png)

[Link to the test file for the failure-inducing input](/testfilesforreport2/test-file3.md)

Symptom of the failure-inducing input:

![Image](/lab2week4ss/Figure2.png)

The failure-inducing input is a string of links that do not contain brackets `[]`. The bug was that it was searching for the open brackets `[` and the closing bracket `]` but it couldn't find any so `nextOpenBracket` and `nextCloseBracket` is `-1`. This then affects `openParen` because it starts searching at `nextCloseBracket` which is not a valid index because the value is `-1`. This results in the symptom being an infinite loop.

---

## Code change 2:

![Image](/lab2week4ss/Figure5.png)

[Link to the test file for the failure-inducing input](/testfilesforreport2/test-file4.md)

Symptom of the failure-inducing input:

![Image](/lab2week4ss/Figure4.png)

The failure-inducing input is simply just open and close brackets `[]` with no parenthesis. The bug was that the code `indexOf()` on line 16 *needs* to find the opening parenthesis `(` but it couldn't find any so `openParen` is `-1`. This then affects `closeParen` which depends on the value of `openParen` passed as an argument. Since `openParen = -1`, the value passed is an invalid value because there is no `-1` index. This results in the symptom being an index out of bounds exception being thrown.

---

## Code change 3:
