

# Parameterization in TestNG

This document explains how to pass parameters to tests.

## Methods

- Using `@Parameters` annotation
- Using `@DataProvider` annotation

## Example

```java
@Test(dataProvider = "dataProviderMethod")
public void test(String input) { ... }
```
