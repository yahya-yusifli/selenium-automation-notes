# Creating Page Classes in POM (Page Object Model)

This document explains how to create and structure page classes in a Selenium automation project using the Page Object Model (POM) design pattern.

---

## 1. What is a Page Class?

A page class in POM represents a single web page or screen in the application. It contains:
- Web element locators
- Methods to perform user actions on that page (e.g., enter text, click button)

Each page = 1 Java class.

---

## 2. Basic Page Class Structure

```java
public class LoginPage {
    WebDriver driver;

    // Constructor
    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    // Locators
    By usernameField = By.id("username");
    By passwordField = By.id("password");
    By loginButton = By.id("loginBtn");

    // Actions
    public void enterUsername(String username) {
        driver.findElement(usernameField).sendKeys(username);
    }

    public void enterPassword(String password) {
        driver.findElement(passwordField).sendKeys(password);
    }

    public void clickLogin() {
        driver.findElement(loginButton).click();
    }

    public void login(String username, String password) {
        enterUsername(username);
        enterPassword(password);
        clickLogin();
    }
}
```

---

## 3. Using PageFactory (Optional)

```java
public class LoginPage {
    WebDriver driver;

    @FindBy(id = "username")
    WebElement usernameField;

    @FindBy(id = "password")
    WebElement passwordField;

    @FindBy(id = "loginBtn")
    WebElement loginButton;

    public LoginPage(WebDriver driver) {
        this.driver = driver;
        PageFactory.initElements(driver, this);
    }

    public void login(String username, String password) {
        usernameField.sendKeys(username);
        passwordField.sendKeys(password);
        loginButton.click();
    }
}
```

---

## 4. Where to Store Page Classes

Place page classes under a dedicated `pages/` package or folder:

```
src/test/java
└── pages
    ├── LoginPage.java
    ├── DashboardPage.java
    └── ProductPage.java
```

---

## 5. Using Page Classes in Tests

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
        // Assertions here
    }

    @AfterMethod
    public void tearDown() {
        driver.quit();
    }
}
```

---

## 6. Tips

- Keep each class focused on a single page.
- Use clear method names that describe user actions.
- Reuse page methods across multiple test cases.

---

## Summary

| Topic                    | Description                                      |
|--------------------------|--------------------------------------------------|
| What is a page class     | Represents a single page with actions            |
| Constructor              | Accepts WebDriver and initializes elements       |
| Element locators         | Declared as `By` or `@FindBy`                    |
| Action methods           | Interact with UI (type, click, read)             |
| Usage in test            | Instantiate and call action methods              |
