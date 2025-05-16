## Runner Class and Cucumber options

**runner class and @cucumberoptions explained**

in cucumber, the **runner class** is responsible for launching the test execution. it integrates cucumber with junit or testng, defines configurations, and specifies the locations of feature files and step definitions.

---

**why do we need a runner class?**

* to execute cucumber feature files as junit/testng tests
* to configure how cucumber behaves (plugins, reports, filters, etc.)
* to define where step definitions and features are located

---

**basic runner class structure**

```java
@RunWith(Cucumber.class)
@CucumberOptions(
    features = "src/test/resources/features",
    glue = "stepdefinitions",
    plugin = {"pretty", "html:target/cucumber-reports"},
    monochrome = true,
    tags = "@smoke"
)
public class TestRunner {
}
```

---

**@runwith(cucumber.class)**

* tells junit to run this test using cucumber's `cucumber.class`.
* required when using cucumber with junit.

---

**@cucumberoptions parameters explained**

| option       | description                                                                 |
| ------------ | --------------------------------------------------------------------------- |
| `features`   | path to the folder where `.feature` files are located                       |
| `glue`       | path to the package containing step definitions and hooks                   |
| `plugin`     | plugins for reporting output (`pretty`, `html`, `json`, etc.)               |
| `monochrome` | if set to `true`, removes extra characters and makes console output cleaner |
| `tags`       | allows filtering of which scenarios to run based on tags                    |

---

**common plugin types**

* `pretty`: formats output in the console
* `html:target/cucumber-reports`: generates an html report in the given path
* `json:target/cucumber.json`: generates a json report
* `junit:target/cucumber.xml`: generates junit-style xml report

---

**example use case: only run smoke tests**

```java
@CucumberOptions(tags = "@smoke")
```

**example use case: run all except regression**

```java
@CucumberOptions(tags = "not @regression")
```

---

**best practices**

* keep only one runner per logical test group (e.g., smoke, regression)
* avoid hardcoding paths — use relative project paths
* place runner class under `src/test/java/runners` for organization
* use `monochrome = true` for clean console output

---

this configuration is essential to connect your cucumber framework with java/junit and organize how scenarios are selected and executed.
