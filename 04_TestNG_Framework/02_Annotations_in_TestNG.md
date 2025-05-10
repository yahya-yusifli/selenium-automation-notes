
# Annotations in TestNG

This document explains the main TestNG annotations, their purposes, and when to use them for organizing and controlling your tests.

---

## What Are Annotations?

In TestNG, annotations are **special markers** you apply to methods or classes that define **how** and **when** they should run during the test execution lifecycle.

They help you:
- Control setup and teardown steps  
- Define dependencies between methods  
- Structure test execution logically

---

## Commonly Used Annotations

###  `@Test`

- **Purpose:** Marks a method as a test case.
- **Details:** Any method with `@Test` will be picked up by TestNG as a test.
- **Example:**
    ```java
    @Test
    public void testLogin() {
        System.out.println("Running login test");
    }
    ```

###  `@BeforeClass`

- **Purpose:** Runs once **before** any `@Test` methods in the current class.
- **Common Use:** Initialize resources needed by all tests in the class (e.g., WebDriver, database connection).
- **Example:**
    ```java
    @BeforeClass
    public void setUp() {
        System.out.println("Setting up resources for class");
    }
    ```

###  `@AfterClass`

- **Purpose:** Runs once **after** all `@Test` methods in the class have run.
- **Common Use:** Cleanup shared resources.
- **Example:**
    ```java
    @AfterClass
    public void tearDown() {
        System.out.println("Cleaning up resources for class");
    }
    ```

###  `@BeforeMethod`

- **Purpose:** Runs **before each** `@Test` method.
- **Common Use:** Reset state or set up test-specific data.
- **Example:**
    ```java
    @BeforeMethod
    public void beforeEachTest() {
        System.out.println("Setting up before each test method");
    }
    ```

###  `@AfterMethod`

- **Purpose:** Runs **after each** `@Test` method.
- **Common Use:** Clean up after individual tests (e.g., logout, reset DB changes).
- **Example:**
    ```java
    @AfterMethod
    public void afterEachTest() {
        System.out.println("Cleaning up after each test method");
    }
    ```

###  `@BeforeSuite`

- **Purpose:** Runs **once before all tests** in the entire suite (`testng.xml` level).
- **Common Use:** Global setup (e.g., starting servers, loading configs).
- **Example:**
    ```java
    @BeforeSuite
    public void beforeSuite() {
        System.out.println("Running global setup before suite");
    }
    ```

###  `@AfterSuite`

- **Purpose:** Runs **once after all tests** in the entire suite.
- **Common Use:** Global teardown (e.g., stopping servers, clearing caches).
- **Example:**
    ```java
    @AfterSuite
    public void afterSuite() {
        System.out.println("Running global cleanup after suite");
    }
    ```

---

## Additional Useful Annotations

###  `@BeforeTest` and `@AfterTest`

- **Purpose:** Run before/after each `<test>` block in `testng.xml`.
- **Example:**
    ```java
    @BeforeTest
    public void beforeTestBlock() {
        System.out.println("Before <test> block in XML");
    }
    ```

###  `@BeforeGroups` and `@AfterGroups`

- **Purpose:** Run before or after specific groups of tests.
- **Example:**
    ```java
    @BeforeGroups("smoke")
    public void beforeSmokeGroup() {
        System.out.println("Setting up for smoke tests");
    }
    ```

---

## Purpose and Benefits

- **Control flow:** You can control the exact sequence of setup and teardown actions.  
- **Avoid duplication:** Shared setup runs once per class or suite, saving time.  
- **Improve clarity:** Teams understand test dependencies and lifecycle easily.  
- **Enable complex setups:** Global vs. local setups are cleanly separated.

---

## Summary Table

| Annotation        | Runs When                                      |
|-------------------|-----------------------------------------------|
| `@BeforeSuite`    | Once before all tests in the suite             |
| `@AfterSuite`     | Once after all tests in the suite              |
| `@BeforeTest`     | Before each `<test>` tag in `testng.xml`       |
| `@AfterTest`      | After each `<test>` tag in `testng.xml`        |
| `@BeforeClass`    | Before the first `@Test` in a class            |
| `@AfterClass`     | After all `@Test`s in a class                  |
| `@BeforeMethod`   | Before each `@Test` method                     |
| `@AfterMethod`    | After each `@Test` method                      |
| `@BeforeGroups`   | Before any test method in the specified group  |
| `@AfterGroups`    | After all test methods in the specified group  |

---


