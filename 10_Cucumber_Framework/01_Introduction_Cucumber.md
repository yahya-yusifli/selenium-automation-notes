# Cucumber BDD Notes

**1. What is Cucumber?**

Cucumber is a BDD (Behavior Driven Development) test automation framework that allows you to write test cases in Gherkin language, a human-readable, domain-specific language.

It helps:

* Bridge communication between business and technical teams
* Automate acceptance tests
* Write readable and executable specifications

**2. Gherkin Syntax**

Gherkin is the language used in Cucumber to define test cases. It uses keywords:

Gherkin Keywords

* **Feature:** Describe the feature under test
* **Scenario:** Define a specific example
* **Given:** Precondition
* **When:** Action/event
* **Then:** Expected outcome
* **And / But:** Used for additional steps

Example

```gherkin
Feature: User Login
  Scenario: Successful Login with valid credentials
    Given User is on the Login Page
    When User enters "john_doe" and "password123"
    And clicks the Login button
    Then User should be redirected to the dashboard
```

**3. Step Definitions**

Step definitions connect Gherkin steps with Java methods using annotations like `@Given`, `@When`, `@Then`, `@And`, and `@But`.

Example:

```java
@Given("^Logged in with username (.+) and password (.+)$")
public void logged_in_username_and_password(String username, String password) {
    loginPage.enterUsername(username);
    loginPage.enterPassword(password);
    loginPage.clickLogin();
}
```

* **(.+)** is used to capture parameters from Gherkin step and pass into the method.

**4. Feature File Structure**

A `.feature` file contains one feature and multiple scenarios.

```gherkin
Feature: Search functionality
  As a user
  I want to search for products
  So that I can find items quickly

  Scenario: Search with valid keyword
    Given User is on the homepage
    When User enters "shoes" into the search input
    And User clicks the search button
    Then Search results should be displayed
```

**5. Scenario Outline**

`Scenario Outline` is used for data-driven testing. It allows running the same scenario with multiple sets of data.

```gherkin
Scenario Outline: Login with different credentials
  Given I entered username <username> and password <password>
  When I press login
  Then I should see the homepage

Examples:
  | username  | password   |
  | john      | 123456     |
  | alice     | pass123    |
```

**6. Hooks**

Hooks are blocks of code that run before or after each scenario.

```java
@Before
public void setUp() {
    driver = new ChromeDriver();
    driver.manage().window().maximize();
}

@After
public void tearDown() {
    driver.quit();
}
```

**7. Runner Class**

Runner class uses `@CucumberOptions` to specify location of step definitions and feature files.

```java
@RunWith(Cucumber.class)
@CucumberOptions(
  features = "src/test/resources/features",
  glue = "stepDefinitions",
  plugin = {"pretty", "html:target/cucumber-reports"},
  monochrome = true
)
public class TestRunner {
}
```

**8. Integration with TestNG / JUnit**

You can use JUnit or TestNG as test runners. Cucumber hooks and reports can be combined with them for parallel execution and enhanced logging.

---

