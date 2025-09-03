## Cucumber parallel execution

cucumber can be configured to run scenarios in parallel using testng or junit. this significantly reduces test execution time by running multiple scenarios or features at the same time.

---

**why use parallel execution?**

* reduces overall test duration
* enables better utilization of resources (cpu/cores)
* essential for large test suites in ci pipelines

---

**approach 1: parallel execution with testng**

1. create a testng xml suite:

```xml
<suite name="parallel-feature-suite" parallel="tests" thread-count="3">
    <test name="feature1">
        <classes>
            <class name="runners.Runner1" />
        </classes>
    </test>
    <test name="feature2">
        <classes>
            <class name="runners.Runner2" />
        </classes>
    </test>
</suite>
```

2. create separate runner classes for each feature file:

```java
@RunWith(Cucumber.class)
@CucumberOptions(
    features = "src/test/resources/features/login.feature",
    glue = "stepdefinitions",
    plugin = {"pretty", "html:target/report-login"}
)
public class Runner1 {}
```

---

**approach 2: parallel execution with junit and cucumber 6+**

use the `@suite` and `@selectclasses` annotations:

```java
@RunWith(ParallelSuite.class)
@Suite.SuiteClasses({
    Runner1.class,
    Runner2.class
})
public class ParallelTestSuite {}
```

or use maven with surefire plugin:

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>3.0.0</version>
    <configuration>
        <parallel>classes</parallel>
        <threadCount>3</threadCount>
    </configuration>
</plugin>
```

---

**best practices**

* avoid shared state between steps (use thread-local or dependency injection)
* isolate test data per thread
* group features by speed to balance load across threads
* keep reporting separate per thread to avoid data clashes

---

**summary**
parallel execution in cucumber boosts performance, especially in large-scale testing environments. configure your runners and build tool properly, and follow isolation best practices to prevent flaky tests.
