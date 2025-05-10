# Parallel Testing in TestNG

## What is Parallel Testing?

Parallel testing allows you to run multiple tests, classes, or methods **at the same time** rather than sequentially. This reduces total execution time and improves efficiency, especially for large test suites.

TestNG supports parallelism at several levels:
- Tests
- Classes
- Methods
- Suites

---

## How to Enable Parallel Execution

You configure parallel execution in the `testng.xml` file using the `parallel` attribute and set the `thread-count`.

### Example Configuration

```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="ParallelSuite" parallel="classes" thread-count="2">
    <test name="ParallelTest">
        <classes>
            <class name="tests.TestClass1" />
            <class name="tests.TestClass2" />
        </classes>
    </test>
</suite>
```

- **parallel="classes"** → Runs different test classes in parallel.
- **thread-count="2"** → Uses two threads.

---

## Parallel Levels Explained

| Level      | Description                                      |
|------------|--------------------------------------------------|
| `methods` | Executes test methods in parallel in the same class. |
| `classes` | Executes multiple classes in parallel.            |
| `tests`   | Executes multiple `<test>` blocks in parallel.    |
| `suites`  | Executes multiple suite files in parallel.        |

---

## Example Java Test Classes

```java
// TestClass1.java
public class TestClass1 {
    @Test
    public void testMethod1() {
        System.out.println("TestClass1 - testMethod1 - Thread: " + Thread.currentThread().getId());
    }
}

// TestClass2.java
public class TestClass2 {
    @Test
    public void testMethod2() {
        System.out.println("TestClass2 - testMethod2 - Thread: " + Thread.currentThread().getId());
    }
}
```

**Expected Console Output:**
```
TestClass1 - testMethod1 - Thread: 12
TestClass2 - testMethod2 - Thread: 13
```

This shows that the two classes ran on different threads in parallel.

---

## Best Practices

- **Avoid shared state:** Tests running in parallel should not modify shared data.
- **Use thread-safe resources:** Ensure WebDriver or any shared object is thread-safe or instantiated per thread.
- **Configure thread count carefully:** Too high a thread count can overwhelm your machine.
- **Use parallel execution only when needed:** Not all tests benefit; apply where real time-saving gains exist.

---

## Summary

- Parallel testing boosts speed but requires careful design.
- Configure parallel mode and thread count in `testng.xml`.
- Ensure thread safety to avoid flaky or inconsistent test results.
