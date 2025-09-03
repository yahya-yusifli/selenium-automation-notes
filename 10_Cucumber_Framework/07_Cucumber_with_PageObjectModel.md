## Cucumber with page object model (pom)**

---

**what is page object model (pom)?**
page object model is a design pattern that helps you create object-oriented classes for different pages of your application. each class holds web element locators and reusable methods for interactions on that page.

---

**why use pom with cucumber?**

* improves readability and reusability of test code
* separates test logic from element locators and actions
* simplifies maintenance when the ui changes
* supports better project organization

---

**recommended structure**

```
src/test/java
├── pages/               # page classes for each web page
├── stepdefinitions/     # glue code (step definitions)
├── features/           # .feature files
├── runners/            # cucumber test runners
```

---

**example: login.feature**

```gherkin
feature: user login

  scenario: successful login
    given user is on the login page
    when user enters valid username and password
    then user should be redirected to the homepage
```

---

**loginpage.java (in pages/)**

```java
public class LoginPage {
    private WebDriver driver;

    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    private By usernameField = By.id("username");
    private By passwordField = By.id("password");
    private By loginButton = By.id("login");

    public void enterUsername(String username) {
        driver.findElement(usernameField).sendKeys(username);
    }

    public void enterPassword(String password) {
        driver.findElement(passwordField).sendKeys(password);
    }

    public void clickLogin() {
        driver.findElement(loginButton).click();
    }
}
```

---

**loginsteps.java (in stepdefinitions/)**

```java
public class LoginSteps {
    WebDriver driver = new ChromeDriver();
    LoginPage loginPage = new LoginPage(driver);

    @Given("user is on the login page")
    public void navigateToLoginPage() {
        driver.get("https://example.com/login");
    }

    @When("user enters valid username and password")
    public void enterCredentials() {
        loginPage.enterUsername("admin");
        loginPage.enterPassword("admin123");
        loginPage.clickLogin();
    }

    @Then("user should be redirected to the homepage")
    public void verifyHomePage() {
        Assert.assertTrue(driver.getCurrentUrl().contains("dashboard"));
    }
}
```

---

**benefits of this structure**

* page methods can be reused in different scenarios
* changes to locators require updates in one place only
* enhances readability for non-technical stakeholders

---

**best practices**

* name page classes and step definitions clearly (e.g., `LoginPage`, `LoginSteps`)
* avoid putting selenium logic inside step definitions directly
* use constructors to pass the `WebDriver` to page classes
* centralize browser setup using `hooks` or `base test` class

---

this integration pattern keeps your cucumber project scalable and clean for long-term test automation.
