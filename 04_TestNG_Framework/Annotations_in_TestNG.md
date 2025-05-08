# Annotations in TestNG

This document explains the main TestNG annotations and their purpose.

## Common Annotations

- `@Test`: Marks a method as a test method.
- `@BeforeClass`: Runs once before the first method in the current class.
- `@AfterClass`: Runs once after all methods in the current class.
- `@BeforeMethod`: Runs before each `@Test` method.
- `@AfterMethod`: Runs after each `@Test` method.
- `@BeforeSuite`: Runs once before all tests in the suite.
- `@AfterSuite`: Runs once after all tests in the suite.

## Purpose

Annotations control the flow and setup of tests, making test execution predictable and organized.
