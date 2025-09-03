# Creating Test Classes in Selenium with TestNG and POM

This document explains how to properly create and structure test classes in a Selenium framework using TestNG and the Page Object Model (POM) design pattern.

---

## 1. What Is a Test Class?

A test class:
- Contains actual `@Test` methods.
- Calls methods from corresponding page classes.
- Contains setup (`@BeforeMethod`) and teardown (`@AfterMethod`) for browser/session handling.

Each test class generally corresponds to a specific feature or workflow.

---

## 2. Basic Structure of a Test Class

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.*;
import pages.LoginPage;

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
        // Assert dashboard appears or user is logged in
    }

    @AfterMethod
    public void tearDown() {
        driver.quit();
    }
}
```

---

## 3. Best Practices

### a. Use One Test Class per Feature
- Example: `LoginTest.java`, `SearchTest.java`, `CheckoutTest.java`

### b. Avoid Logic in Test Class
- Test class should only **call page methods** and assert results.

### c. Use Assertions in Test Classes
- Do not include assertions in page classes.
```java
Assert.assertTrue(dashboardPage.getWelcomeText().contains("Welcome"));
```

### d. Parameterize Test Data
- Use `@DataProvider` or config files to pass test data.

### e. Name Methods Clearly
- `testLoginWithValidCredentials()` is better than `test1()`

### f. Group Related Tests
```java
@Test(groups = {"sanity"})
public void testSearchFeature() {
    ...
}
```

---

## 4. Example with Assertions and Grouping

```java
@Test(priority = 1, groups = {"regression", "smoke"})
public void loginShouldSucceedWithValidCredentials() {
    loginPage.login("admin", "admin123");
    String dashboardText = driver.findElement(By.id("welcome")).getText();
    Assert.assertTrue(dashboardText.contains("Welcome"));
}
```

---

## 5. Recommended Folder Structure

```
src/test/java
├── pages/
│   └── LoginPage.java
│
├── tests/
│   ├── LoginTest.java
│   ├── SearchTest.java
│
├── utils/
│   └── WebDriverFactory.java
```

---

## Summary

| Section               | Description                                      |
|-----------------------|--------------------------------------------------|
| Test Class Purpose    | Contains `@Test` and test-specific logic         |
| Setup and Teardown    | Managed via `@BeforeMethod` and `@AfterMethod`  |
| Assertion Location    | Keep assertions in test class only              |
| Reusability           | Delegate actions to page classes                |
| Project Structure     | Organize test classes under `/tests` directory  |
