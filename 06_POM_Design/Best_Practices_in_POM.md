# Best Practices in Page Object Model (POM)

This document outlines key best practices for implementing the Page Object Model (POM) in Selenium test automation.

---

## 1. One Class Per Page
- Create a separate Java class for each web page (e.g., `LoginPage.java`, `DashboardPage.java`).
- Keeps element locators and methods organized and focused.

---

## 2. Keep Locators Private and Final (Where Possible)
```java
private final By usernameField = By.id("username");
```
- Prevents unwanted modifications.
- Encourages encapsulation and consistent use of locators.

---

## 3. Create Clear and Actionable Methods
- Use descriptive method names like `login()`, `enterUsername()`, `clickLoginButton()`.
- Methods should represent user actions.

```java
public void login(String username, String password) {
    enterUsername(username);
    enterPassword(password);
    clickLoginButton();
}
```

---

## 4. Avoid Test Logic in Page Classes
- Page classes should focus on interacting with the UI only.
- Keep assertions and test logic in test classes.

---

## 5. Use PageFactory for Better Readability (Optional)
```java
@FindBy(id = "username")
WebElement usernameField;
```
- Reduces `findElement()` calls and improves clarity.
- Use with `PageFactory.initElements(driver, this);`

---

## 6. Return Page Objects After Navigation
```java
public DashboardPage clickLoginButton() {
    loginButton.click();
    return new DashboardPage(driver);
}
```
- Enables method chaining and page flow modeling.

---

## 7. Add Waits for Stability
- Use explicit waits inside page methods where necessary.
```java
wait.until(ExpectedConditions.visibilityOf(usernameField)).sendKeys(username);
```

---

## 8. Organize POM Structure Cleanly
**Suggested Project Structure:**
```
src/test/java
│
├── pages/
│   ├── LoginPage.java
│   ├── DashboardPage.java
│
├── tests/
│   ├── LoginTest.java
│
├── utils/
│   ├── WebDriverFactory.java
```

---

## 9. Reuse and Centralize Common Code
- Centralize driver setup, waits, and configurations in utility or base classes.

---

## 10. Use Meaningful Naming Conventions
- Name locators and methods based on their function and UI behavior.

```java
private final By searchInput = By.id("search-box");
public void enterSearchQuery(String query) { ... }
```

---

## Summary

| Practice                       | Benefit                                         |
|--------------------------------|--------------------------------------------------|
| One class per page             | Clear organization                              |
| Encapsulate locators           | Protect and standardize access                  |
| Descriptive methods            | Improves code readability                       |
| Keep logic out of page class   | Ensures clear separation of concerns            |
| Use PageFactory (optional)     | Simplifies code                                 |
| Return new page objects        | Models user flow cleanly                        |
| Use waits                      | Increases test stability                        |
| Clean project structure        | Scales well with team and codebase              |
| Centralized utilities          | Reduces code duplication                        |
| Meaningful naming              | Better maintainability                          |

