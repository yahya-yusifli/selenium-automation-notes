## Cucumber

**what is cucumber?**
cucumber is a behavior-driven development (bdd) testing framework that allows writing test cases in plain language using **gherkin syntax**. it helps bridge the communication gap between technical and non-technical stakeholders (like qa, devs, and business analysts).

---

**why use cucumber?**

* enables non-programmers to understand and contribute to test cases
* acts as **live documentation** of the system's behavior
* improves collaboration in agile teams
* integrates easily with selenium, junit, testng, and maven
* supports **data-driven testing** using scenario outlines

---

**core components**

| component        | role                                                               |
| ---------------- | ------------------------------------------------------------------ |
| feature          | describes a feature or functionality in business terms             |
| scenario         | one test example or use case                                       |
| scenario outline | template scenario with placeholders and example data               |
| step definition  | maps gherkin steps to java methods with selenium/test logic        |
| hook             | setup or teardown code that runs before/after each scenario        |
| runner           | test runner class that connects cucumber to junit/testng framework |

---

**gherkin syntax keywords**

* `feature`: describes the overall functionality being tested
* `scenario`: defines a concrete use case or user interaction
* `given`: precondition step
* `when`: main action the user takes
* `then`: expected result
* `and` / `but`: additional conditions

**example feature file**

```gherkin
feature: login feature

  scenario: valid login
    given user is on login page
    when user enters valid credentials
    then user should be redirected to homepage
```

---

**step definitions in java**

```java
@Given("user is on login page")
public void user_on_login_page() {
    driver.get("https://example.com/login");
}

@When("user enters valid credentials")
public void user_enters_valid_credentials() {
    driver.findElement(By.id("email")).sendKeys("user@example.com");
    driver.findElement(By.id("password")).sendKeys("123456");
    driver.findElement(By.id("loginButton")).click();
}

@Then("user should be redirected to homepage")
public void redirected_to_homepage() {
    Assert.assertTrue(driver.getCurrentUrl().contains("homepage"));
}
```

---

**scenario outline (data-driven)**

```gherkin
scenario outline: login with valid and invalid users
  given user is on login page
  when user enters "<username>" and "<password>"
  then user should see "<result>"

examples:
  | username      | password | result   |
  | valid_user    | 123456   | success  |
  | invalid_user  | 000000   | failure  |
```

---

**runner class using junit**

```java
@RunWith(Cucumber.class)
@CucumberOptions(
    features = "src/test/resources/features",
    glue = "stepdefinitions",
    plugin = {"pretty", "html:target/cucumber-report.html"},
    monochrome = true
)
public class TestRunner {}
```

---

**hooks: setup and teardown**

```java
@Before
public void setup() {
    driver = new ChromeDriver();
    driver.manage().window().maximize();
}

@After
public void teardown() {
    driver.quit();
}
```

---

**using tags to control execution**

```gherkin
@smoke
scenario: verify login works
```

```java
@CucumberOptions(tags = "@smoke")
```

---

**reporting options**

* built-in: `pretty`, `html`, `json`, `junit`
* external: `extentReports`, `allure`

---

**best practices**

* use page object model (pom) for cleaner code
* reuse step definitions instead of duplicating logic
* avoid technical jargon in gherkin steps
* don't mix UI locators or logic in .feature files
* tag scenarios based on test type: `@smoke`, `@regression`, `@login`

---

**summary**
cucumber empowers teams to write **readable, maintainable, and executable specifications** for system behavior. its ability to map human-readable language to test logic helps ensure that everyone on the team understands what’s being tested and why.
