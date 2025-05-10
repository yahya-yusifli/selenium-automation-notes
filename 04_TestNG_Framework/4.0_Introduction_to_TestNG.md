# Introduction to TestNG


## What is TestNG?

TestNG (Test Next Generation) is a Java testing framework inspired by JUnit and NUnit but designed with additional powerful features:
- Supports annotations (@Test, @BeforeMethod, etc.)
- Allows test grouping and prioritization
- Provides parallel test execution
- Generates detailed HTML reports
- Handles data-driven testing with `@DataProvider`
- Supports dependency between tests

---

## Why Use TestNG?

- **Organized Test Execution:** Define test flow using annotations.
- **Flexible Configuration:** Control which tests run and how using `testng.xml`.
- **Advanced Reporting:** Get structured pass/fail/skipped reports.
- **Integration-Friendly:** Works well with build tools like Maven, Gradle, and CI tools like Jenkins.

---

## Basic TestNG Annotations

| Annotation          | Purpose                                                            |
|---------------------|-------------------------------------------------------------------|
| @Test              | Marks a method as a test method.                                  |
| @BeforeMethod      | Runs before each `@Test` method.                                  |
| @AfterMethod       | Runs after each `@Test` method.                                   |
| @BeforeClass       | Runs once before the first test in the current class.             |
| @AfterClass        | Runs once after all tests in the current class.                  |
| @BeforeSuite       | Runs once before all tests in the entire suite.                  |
| @AfterSuite        | Runs once after all tests in the entire suite.                   |

---

## Example TestNG Test Class

```java
import org.testng.annotations.*;

public class SampleTest {

    @BeforeClass
    public void setupClass() {
        System.out.println("BeforeClass: Setup resources");
    }

    @BeforeMethod
    public void setupTest() {
        System.out.println("BeforeMethod: Setup before each test");
    }

    @Test
    public void testLogin() {
        System.out.println("Executing testLogin");
    }

    @Test
    public void testLogout() {
        System.out.println("Executing testLogout");
    }

    @AfterMethod
    public void tearDownTest() {
        System.out.println("AfterMethod: Cleanup after each test");
    }

    @AfterClass
    public void tearDownClass() {
        System.out.println("AfterClass: Release resources");
    }
}
```

**Expected Console Output:**
```
BeforeClass: Setup resources
BeforeMethod: Setup before each test
Executing testLogin
AfterMethod: Cleanup after each test
BeforeMethod: Setup before each test
Executing testLogout
AfterMethod: Cleanup after each test
AfterClass: Release resources
```

---

## Running Tests with testng.xml

Create a `testng.xml` file:

```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="MySuite">
    <test name="MyTests">
        <classes>
            <class name="SampleTest" />
        </classes>
    </test>
</suite>
```

- Right-click the `testng.xml` in IntelliJ → Run.
- TestNG will execute all listed classes and generate a report.

---

## Summary

- TestNG simplifies Java test management.
- Supports powerful features like grouping, data-driven testing, and parallel runs.
- Works well with Selenium for automated web testing.
