# Lab Report 2 Week 4
---
## Code change 1:

![Image](/lab2week4ss/Figure3.png)

[Link to the test file for the failure-inducing input](test-file3.md)

Symptom of the failure-inducing input:

![Image](/lab2week4ss/Figure2.png)

The failure-inducing input is a string of links that do not contain brackets `[]`. The bug was that it was searching for the open brackets `[` and the closing bracket `]` but it couldn't find any so `nextOpenBracket` and `nextCloseBracket` is `-1`. This then affects `openParen` because it starts searching at `nextCloseBracket` which is not a valid index because the value is `-1`. This results in the symptom being an infinite loop.

## Code change 2:
