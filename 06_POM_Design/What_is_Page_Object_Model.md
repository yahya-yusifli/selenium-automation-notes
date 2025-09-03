# What is Page Object Model (POM)?

The Page Object Model (POM) is a design pattern used in Selenium automation testing to create an object repository for web elements. It helps in building robust, maintainable, and scalable test frameworks.

---

## Definition

POM is a design approach where each web page in the application is represented by a separate Java class. This class contains:
- Web element locators
- Methods that perform actions on those elements

---

## Why Use POM?

- **Separation of concerns** between test logic and element locators
- **Improved readability and reusability**
- **Centralized management** of locators and actions
- **Scalability** for larger test suites

---

## Key Components

| Component     | Role                                                   |
|---------------|--------------------------------------------------------|
| Page Class    | Represents a web page, defines locators + methods     |
| Test Class    | Contains test cases and calls methods from page class |
| Locators      | Defined using `By` or `@FindBy` for web elements      |

---

## Simple POM Example

### LoginPage.java
```java
public class LoginPage {
    WebDriver driver;

    By username = By.id("username");
    By password = By.id("password");
    By loginBtn = By.id("loginBtn");

    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    public void login(String user, String pass) {
        driver.findElement(username).sendKeys(user);
        driver.findElement(password).sendKeys(pass);
        driver.findElement(loginBtn).click();
    }
}
```

### LoginTest.java
```java
public class LoginTest {
    WebDriver driver;
    LoginPage loginPage;

    @BeforeMethod
    public void setup() {
        driver = new ChromeDriver();
        driver.get("https://example.com/login");
        loginPage = new LoginPage(driver);
    }

    @Test
    public void validLoginTest() {
        loginPage.login("admin", "admin123");
    }

    @AfterMethod
    public void tearDown() {
        driver.quit();
    }
}
```

---

## Advantages of POM

- Changes to the UI are easier to manage.
- Encourages reuse of methods and test data.
- Makes code modular and easy to debug.
- Compatible with frameworks like TestNG, JUnit, Cucumber.

---

## When to Use POM

- For medium to large Selenium projects
- When you need to reuse steps across multiple test cases
- When maintainability and scalability are important

---

## Summary

| Feature         | Description                                     |
|-----------------|-------------------------------------------------|
| Test Separation | Test code is separate from page structure       |
| Page Classes    | Encapsulate locators and UI actions             |
| Reusability     | Same page methods used in multiple test cases   |
| Maintainability | Update locators in one place                    |
