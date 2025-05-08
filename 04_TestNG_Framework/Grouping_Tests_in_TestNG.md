# Grouping Tests in TestNG

This document explains how to group and run specific sets of tests.

## Defining Groups

You can assign tests to groups using:

```java
@Test(groups = { "regression", "smoke" })
public void testMethod() { ... }
```

## Running Groups

Configure groups in the testng.xml file or via the command line.

## Purpose

Group tests by feature, purpose, or priority for better organization.
