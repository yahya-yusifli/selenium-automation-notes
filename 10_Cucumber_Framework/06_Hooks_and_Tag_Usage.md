## Hooks and tag usage in cucumber

cucumber allows you to define reusable setup and teardown logic using **hooks**, and organize/select test cases using **tags**.

---

**what are hooks?**
hooks are blocks of code that run **before** or **after** each scenario. they are defined in separate java classes under the `stepdefinitions` or `hooks` package.

**available hooks:**

* `@before` → runs before each scenario
* `@after` → runs after each scenario
* `@beforestep` → runs before every step
* `@afterstep` → runs after every step

**example: basic hooks**

```java
@Before
public void setUp() {
    // open browser
    driver = new ChromeDriver();
    driver.manage().window().maximize();
}

@After
public void tearDown() {
    // close browser
    driver.quit();
}
```

**example: conditional hook using tags**

```java
@Before("@db")
public void setUpDatabase() {
    // only runs before scenarios tagged with @db
    connectToDatabase();
}
```

---

**what are tags?**
tags are used to label and organize your scenarios. they help you:

* filter which tests to run
* group tests (e.g. @smoke, @regression)

**tagging scenarios**

```gherkin
@smoke
scenario: user logs in with valid credentials
```

**tagging feature files**

```gherkin
@regression
feature: login functionality
```

**tag expressions in runner class**

```java
@CucumberOptions(
  features = "src/test/resources/features",
  glue = "stepdefinitions",
  tags = "@smoke",
  plugin = {"pretty", "html:target/report.html"},
  monochrome = true
)
```

**tag filter examples:**

* `@CucumberOptions(tags = "@smoke")` → runs only @smoke
* `@CucumberOptions(tags = "@smoke and @regression")` → must have both tags
* `@CucumberOptions(tags = "@smoke or @regression")` → runs either tag
* `@CucumberOptions(tags = "not @skip")` → exclude @skip tests

---

**best practices**

* use meaningful tags like `@login`, `@checkout`, `@critical`
* avoid over-tagging every test
* isolate browser setup/cleanup logic in hooks
* separate environment-specific logic using conditional hooks

---

## Cucumber with page object model (pom)

---

**what is page object model?**
page object model (pom) is a design pattern used in test automation to create an object repository for web ui elements. it helps separate the page structure from test logic, improving reusability and maintainability.

in cucumber, pom is combined with step definitions so that each page interaction is handled by dedicated java classes.

---

**why use pom with cucumber?**

* separates concerns: feature file, step definition, and page actions are all separate
* increases reusability of element locators and methods
* makes code easier to maintain as ui changes
* follows clean code and oops principles

---

**project structure**

```
src/test/java
├── features/                   # .feature files
├── stepdefinitions/            # step definition files
├── pages/                      # page classes (pom)
├── runners/                    # test runner class
└── utils/                      # driver setup and config
```

---

**sample feature file**

```gherkin
feature: login functionality

  scenario: successful login
    given user is on the login page
    when user enters valid credentials
    then user should be redirected to the dashboard
```

---

**loginpage.java (page class)**

```java
public class LoginPage {
    WebDriver driver;

    public LoginPage(WebDriver driver) {
        this.driver = driver;
        PageFactory.initElements(driver, this);
    }

    @FindBy(id = "email")
    public WebElement emailField;

    @FindBy(id = "password")
    public WebElement passwordField;

    @FindBy(id = "submit")
    public WebElement loginButton;

    public void enterEmail(String email) {
        emailField.sendKeys(email);
    }

    public void enterPassword(String password) {
        passwordField.sendKeys(password);
    }

    public void clickLogin() {
        loginButton.click();
    }
}
```

---

**loginsteps.java (step definition)**

```java
public class LoginSteps {
    WebDriver driver;
    LoginPage loginPage;

    @Given("user is on the login page")
    public void user_is_on_login_page() {
        driver = DriverFactory.getDriver();
        driver.get("https://example.com/login");
        loginPage = new LoginPage(driver);
    }

    @When("user enters valid credentials")
    public void user_enters_valid_credentials() {
        loginPage.enterEmail("test@example.com");
        loginPage.enterPassword("123456");
        loginPage.clickLogin();
    }

    @Then("user should be redirected to the dashboard")
    public void user_should_be_redirected() {
        Assert.assertTrue(driver.getCurrentUrl().contains("dashboard"));
    }
}
```

---

**benefits of this approach**

* changes in ui affect only page classes, not step definitions
* avoids duplicate code across step files
* better organized and scalable for large test suites
