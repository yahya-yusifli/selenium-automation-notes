# Parallel Testing in TestNG

This document explains how to run tests in parallel.

## How to Configure

- Use `parallel` and `thread-count` attributes in `testng.xml`.
- Example:

```xml
<suite name="ParallelSuite" parallel="tests" thread-count="2">
    ...
</suite>
