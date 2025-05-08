
# Grouping Tests in TestNG

This document explains how to group, organize, and run specific sets of tests in TestNG.

---

## What Are TestNG Groups?

TestNG **groups** allow you to organize tests into categories so you can run specific subsets as needed.  
This is especially useful in large test suites where you don’t want to execute every test every time.

You can group tests by:
- Feature area (e.g., login, checkout, payment)
- Type (e.g., smoke, regression, sanity)
- Priority or importance (e.g., critical, optional)
- Team responsibility (e.g., frontend, backend, integration)

---

## Defining Groups in Code

Assign one or more groups to a test using the `groups` attribute:

```java
@Test(groups = { "regression", "smoke" })
public void testMethod() {
    // test code here
}
```

 **Notes:**
- A test can belong to **multiple groups**.
- You can apply groups at the **class level** too:
  
```java
@Test(groups = { "api-tests" })
public class ApiTestSuite {
    // all methods here belong to 'api-tests' group
}
```

---

## Running Specific Groups

You can configure TestNG to **include** or **exclude** groups via `testng.xml`.

### Example: Including Groups

```xml
<test name="Regression and Smoke Tests">
    <groups>
        <run>
            <include name="regression"/>
            <include name="smoke"/>
        </run>
    </groups>
    <classes>
        <class name="com.example.tests.MyTestClass"/>
    </classes>
</test>
```

### Example: Excluding Groups

```xml
<groups>
    <run>
        <exclude name="slow-tests"/>
    </run>
</groups>
```

---

## Running Groups from Command Line

You can run specific groups without editing `testng.xml` using the command line:

```
java -cp <classpath> org.testng.TestNG -groups regression,smoke testng.xml
```

Or to exclude groups:

```
java -cp <classpath> org.testng.TestNG -excludegroups slow-tests testng.xml
```

---

## Group Dependencies

TestNG also allows you to define **group dependencies**.

Example:

```java
@Test(groups = {"database"}, dependsOnGroups = {"init"})
public void testDatabaseQuery() {
    // runs only after all 'init' group tests are complete
}
```

 **Important:**
- Dependencies ensure that setup or prerequisite groups finish before dependent groups run.
- If a dependency fails, the dependent group will be skipped.

---

## Best Practices

- Use **clear, consistent group names** (e.g., lowercase, dash-separated).
- Avoid overusing groups—group only when you need selective execution.
- Document your group names and their purpose in your project README or wiki.
- Combine groups with Maven or CI tools (like Jenkins) to run the right tests in the right pipeline stages.

---

## Common Group Examples

| Group Name   | Purpose                                     |
|--------------|--------------------------------------------|
| `smoke`      | Basic system checks to ensure major flows work |
| `regression` | Full set of tests to detect side effects    |
| `sanity`     | Quick checks on new features or patches     |
| `critical`   | High-priority business or customer flows    |
| `slow-tests` | Tests that take long and may run separately |

---

