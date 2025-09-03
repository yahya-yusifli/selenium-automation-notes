
# PageFactory and @FindBy Annotations in Selenium

This document explains how to use `PageFactory` and `@FindBy` annotations in Selenium with the Page Object Model (POM) design pattern.

---

## What is PageFactory?

`PageFactory` is a Selenium class that supports the **initialization of elements** defined using `@FindBy` annotations.

- Helps avoid repetitive `driver.findElement()` calls.
- Makes code cleaner and easier to read.
- Elements are **lazy-initialized**, meaning they are found only when used.

---

## How to Use PageFactory

### Step 1: Define WebElements Using @FindBy
```java
@FindBy(id = "username")
WebElement usernameInput;

@FindBy(id = "password")
WebElement passwordInput;

@FindBy(id = "loginBtn")
WebElement loginButton;
```

### Step 2: Initialize Elements in Constructor
```java
public LoginPage(WebDriver driver) {
    this.driver = driver;
    PageFactory.initElements(driver, this);
}
```

---

## Complete Example

```java
public class LoginPage {

    WebDriver driver;

    @FindBy(id = "username")
    WebElement usernameInput;

    @FindBy(id = "password")
    WebElement passwordInput;

    @FindBy(id = "loginBtn")
    WebElement loginButton;

    public LoginPage(WebDriver driver) {
        this.driver = driver;
        PageFactory.initElements(driver, this);
    }

    public void login(String username, String password) {
        usernameInput.sendKeys(username);
        passwordInput.sendKeys(password);
        loginButton.click();
    }
}
```

---

## Supported @FindBy Strategies

| Strategy     | Syntax Example                              |
|--------------|----------------------------------------------|
| id           | `@FindBy(id = "login")`                     |
| name         | `@FindBy(name = "username")`               |
| className    | `@FindBy(className = "input-field")`       |
| tagName      | `@FindBy(tagName = "input")`               |
| linkText     | `@FindBy(linkText = "Forgot Password")`    |
| partialLinkText | `@FindBy(partialLinkText = "Forgot")`   |
| css          | `@FindBy(css = "input[type='text']")`      |
| xpath        | `@FindBy(xpath = "//input[@id='username']")`|

---

## Multiple Locators with @FindBys and @FindAll

### @FindBys (AND condition)
```java
@FindBys({
    @FindBy(className = "form-control"),
    @FindBy(name = "email")
})
WebElement emailField;
```

### @FindAll (OR condition)
```java
@FindAll({
    @FindBy(id = "email"),
    @FindBy(name = "user_email")
})
WebElement emailField;
```

---

## When to Use PageFactory

- When your project follows POM strictly.
- For better readability and element management.
- When you want to reduce repeated `findElement` calls.

---

## When to Avoid

- If you prefer full control with dynamic locators.
- If you rely heavily on runtime strategies.

---

## Summary

| Feature             | Description                                  |
|---------------------|----------------------------------------------|
| PageFactory         | Initializes `@FindBy` annotated elements     |
| @FindBy             | Replaces `driver.findElement(...)`          |
| Lazy Initialization | Elements are not located until they are used|
| Cleaner Code        | No need to call `findElement()` repeatedly  |

