## Cucumber reporting overview

cucumber provides built-in and extendable reporting options that help teams analyze test results, failures, and test coverage. reports can be generated in multiple formats like html, json, junit xml, and more.

---

**1. built-in report plugins**

cucumber offers built-in plugins via the `@cucumberoptions` annotation in the runner class.

**common plugins:**

* `pretty` → prints gherkin steps in console (formatted)
* `html:target/report.html` → generates an html report
* `json:target/report.json` → creates json output for further processing
* `junit:target/report.xml` → creates junit-style xml report

**example:**

```java
@cucumberoptions(
  plugin = {
    "pretty",
    "html:target/cucumber-reports.html",
    "json:target/cucumber.json",
    "junit:target/cucumber.xml"
  }
)
```

---

**2. extent reports integration**

extent reports generate detailed and interactive html reports with logs, steps, and screenshots. cucumber can integrate with extent reports through hooks or listeners.

**basic setup:**

1. add extent reports dependency to `pom.xml`

```xml
<dependency>
  <groupid>com.aventstack</groupid>
  <artifactid>extentreports</artifactid>
  <version>5.0.9</version>
</dependency>
```

2. initialize extent report in a `@before` hook

```java
extent = new extentreports();
sparkreporter reporter = new extentsparkreporter("target/extent-report.html");
extent.attachreporter(reporter);
```

3. log steps in hooks or step definitions

```java
test.log(status.pass, "step passed");
test.fail("step failed with screenshot");
```

---

**3. allure reports**

allure is a popular reporting tool used with cucumber to visualize execution trends, history, screenshots, and attachments.

**setup:**

* install allure command-line
* use plugin: `"io.qameta.allure:allure-cucumber6-jvm"`
* generate reports using: `allure serve target/allure-results`

---

**4. best practices**

* combine html and json reports for both visibility and integration
* capture screenshots in `@after` hooks for failures
* structure reports by feature, scenario, and tags
* clean `target/` folder before test runs to avoid conflicts

---

**summary**
cucumber supports multiple reporting strategies. choose based on team needs:

* for simple reports: built-in html
* for rich visuals: extent or allure
* for ci integration: json or junit xml

always include reporting in your automation pipeline for visibility and debugging.
