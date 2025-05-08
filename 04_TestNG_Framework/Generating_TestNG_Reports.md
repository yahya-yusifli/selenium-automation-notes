
# Generating TestNG Reports

This document explains how to generate, locate, and interpret TestNG test reports for better test result analysis.

---

## Types of Reports

###  HTML Reports

- **Description:** Automatically generated after each TestNG run.
- **Location:** Found under the `test-output` folder (default location).
- **Content:** Shows summary of passed, failed, and skipped tests, grouped by class, method, and suite.
- **Usage:** Open `index.html` in a browser to view a full interactive report.

###  XML Reports

- **Description:** Machine-readable XML files generated alongside HTML reports.
- **Location:** Stored in the `test-output` directory (e.g., `testng-results.xml`).
- **Purpose:** Used for integrations with tools like Jenkins, CI pipelines, or reporting dashboards.
- **Usage:** Feed these XML files into external systems for automated report processing.

###  Custom Reports

- **Description:** Build your own custom reports using TestNG’s listener interfaces (e.g., `IReporter`, `ITestListener`).
- **Example Use Cases:** Generating PDF reports, integrating with external reporting tools, or sending summary emails after a run.
- **Implementation:** Write a custom Java class that implements the listener interface and register it in `testng.xml` or via annotations.

```java
public class MyCustomReporter implements IReporter {
    @Override
    public void generateReport(...) {
        // custom report logic
    }
}
```

In `testng.xml`:

```xml
<listeners>
    <listener class-name="com.example.MyCustomReporter"/>
</listeners>
```

---

## Where to Find Reports

After running your TestNG suite (from IDE or command line), look for the `test-output` directory created in your project’s root.

Key files inside:
- `index.html`: Main HTML report entry
- `emailable-report.html`: Summary report suitable for email
- `testng-results.xml`: Detailed machine-readable results
- `junitreports` folder: Optional JUnit-compatible reports

---

## Purpose of Reports

- Provide **clear communication** of test results to developers, QA, and stakeholders.
- Help **analyze failures** by showing stack traces, failure messages, and logs.
- Support **trend analysis** when integrated into CI/CD pipelines.
- Enable **automated monitoring** when plugged into dashboards or reporting tools.

---

## Enhancing Reports

- Use the `Reporter.log()` method in your test code to add **custom messages** to reports.
- Integrate with **Allure** or **ExtentReports** for richer, more visual reporting.
- Configure listeners to **capture screenshots** on failure and include them in reports.

Example:

```java
Reporter.log("Starting login test...");  // Will appear in HTML report
```

---

## Best Practices

- Regularly review reports after test runs, especially after failures.  
- Save historical reports for tracking changes over time.  
- Customize reports when default ones do not meet your team’s needs.  
- Share reports with the team using CI/CD pipelines or email notifications.


