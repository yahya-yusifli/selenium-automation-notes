## Cucumber

**what is cucumber?**  
cucumber is a behavior-driven development (bdd) framework that allows writing test scenarios in plain language using gherkin syntax. it enables business stakeholders, qa testers, and developers to collaborate and understand system behavior clearly.

---

**why use cucumber?**  
- bridges communication between technical and non-technical teams  
- promotes agile and test-first development  
- improves readability and traceability of test cases  
- integrates seamlessly with selenium for browser automation  
- supports data-driven testing and reuse of test steps  
- enables living documentation that updates with the product

---

**main components**

| component        | purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| feature          | high-level description of application functionality                     |
| scenario         | individual test case within a feature                                   |
| scenario outline | template for running the same test with multiple data sets              |
| step definition  | java method that maps a gherkin step to executable test code            |
| feature file     | `.feature` file that holds all features, scenarios, and steps           |
| hooks            | code to run before or after a scenario (setup/teardown)                 |
| runner class     | configures cucumber to locate features, step defs, reports, etc.        |

---

**gherkin keywords**  
- `feature:` groups scenarios under a specific business capability  
- `scenario:` defines a test case with given-when-then steps  
- `scenario outline:` allows same test to run with different data  
- `given:` sets up the initial context  
- `when:` performs the main action  
- `then:` verifies the expected outcome  
- `and`, `but:` support multiple steps in a flow

---

**gherkin feature file example**

```gherkin
feature: user login

  scenario: successful login
    given user is on the login page
    when user enters valid username and password
    then user should be redirected to the dashboard
```

---

**java step definitions**

```java
@Given("user is on the login page")
public void userOnLoginPage() {
    driver.get("https://example.com/login");
}

@When("user enters valid username and password")
public void enterCredentials() {
    driver.findElement(By.id("email")).sendKeys("test@example.com");
    driver.findElement(By.id("password")).sendKeys("123456");
    driver.findElement(By.id("submit")).click();
}

@Then("user should be redirected to the dashboard")
public void redirectedToDashboard() {
    Assert.assertTrue(driver.getCurrentUrl().contains("dashboard"));
}
```

---

**scenario outline (for data-driven testing)**

```gherkin
scenario outline: login with multiple credentials
  given user is on the login page
  when user enters "<username>" and "<password>"
  then user should see "<message>"

examples:
  | username         | password | message            |
  | test@example.com | 123456   | welcome            |
  | wrong@user.com   | 000000   | invalid credentials |
```

**step definition example:**

```java
@When("user enters {string} and {string}")
public void user_enters_credentials(String username, String password) {
    driver.findElement(By.id("email")).sendKeys(username);
    driver.findElement(By.id("password")).sendKeys(password);
    driver.findElement(By.id("submit")).click();
}

@Then("user should see {string}")
public void user_should_see_message(String expectedMessage) {
    WebElement msg = driver.findElement(By.id("message"));
    Assert.assertTrue(msg.getText().contains(expectedMessage));
}
```

---

**test runner setup**

```java
@RunWith(Cucumber.class)
@CucumberOptions(
    features = "src/test/resources/features",
    glue = {"stepdefinitions", "hooks"},
    plugin = {"pretty", "html:target/cucumber-reports.html", "json:target/report.json"},
    monochrome = true,
    tags = "@regression"
)
public class TestRunner {}
```

---

**hooks for setup and teardown**

```java
@Before
public void setupBrowser() {
    driver = new ChromeDriver();
    driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
    driver.manage().window().maximize();
}

@After
public void closeBrowser() {
    driver.quit();
}
```

---

**using tags to organize tests**

```gherkin
@regression
scenario: user logs in with valid credentials
```

runner class:

```java
@CucumberOptions(tags = "@regression")
```

you can also combine tags:  
- `@CucumberOptions(tags = "@smoke and @regression")`  
- `@CucumberOptions(tags = "@login or @register")`

---

**cucumber reporting options**  
- built-in: pretty, html, json, junit  
- external:  
  - extent reports integration for professional html reports  
  - allure reports for rich interactive test results

---

**advanced tips**  
- store locators in page classes (page object model)  
- modularize steps to increase reusability  
- avoid using Thread.sleep(); use WebDriverWait  
- write short, focused steps — 1 action per step

---

**project structure recommendation**

```
src/test/java
├── features/             # .feature files
├── stepdefinitions/      # java classes for step mapping
├── hooks/                # @Before and @After methods
├── runners/              # cucumber runner classes
├── pages/                # pom classes for selenium actions
└── utils/                # utility classes (config reader, driver setup)
```

---

**summary**  
cucumber is more than just a testing tool; it supports full specification by example, making test scenarios a collaborative bridge between requirements and automation. with proper structure, step reuse, and integration with selenium, it can drive robust bdd testing in any agile project.
