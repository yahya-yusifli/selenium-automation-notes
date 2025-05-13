# Basic WebElement Actions in Selenium WebDriver

This document explains the most commonly used WebElement actions in Selenium for interacting with elements on a webpage.

---

## 1. Click
Click on a button, checkbox, link, or any clickable element.
```java
driver.findElement(By.id("submitBtn")).click();
```

---

## 2. Send Keys (Typing into Input Field)
Used for entering text into input boxes.
```java
driver.findElement(By.name("username")).sendKeys("myUsername");
```

---

## 3. Clear Input Field
Clears any existing text from a text box.
```java
driver.findElement(By.id("email")).clear();
```

---

## 4. Get Text from Element
Retrieves the visible text content of a WebElement.
```java
String message = driver.findElement(By.id("message")).getText();
System.out.println("Message: " + message);
```

---

## 5. Get Attribute Value
Reads the value of any HTML attribute (e.g., placeholder, value).
```java
String placeholder = driver.findElement(By.id("email")).getAttribute("placeholder");
```

---

## 6. Is Displayed
Checks if an element is present and visible.
```java
boolean visible = driver.findElement(By.id("logo")).isDisplayed();
```

---

## 7. Is Enabled
Checks if a form element is enabled (can be interacted with).
```java
boolean enabled = driver.findElement(By.id("submitBtn")).isEnabled();
```

---

## 8. Is Selected
Checks if a checkbox or radio button is selected.
```java
boolean selected = driver.findElement(By.id("termsCheckbox")).isSelected();
```

---

## 9. Submit Form
Submits a form if the element is inside a `<form>`.
```java
driver.findElement(By.id("loginForm")).submit();
```

---

## Example: Using Multiple Actions Together
```java
WebElement emailInput = driver.findElement(By.id("email"));
emailInput.clear();
emailInput.sendKeys("example@domain.com");

WebElement loginBtn = driver.findElement(By.id("submit"));
if (loginBtn.isEnabled()) {
    loginBtn.click();
}
```

---

## Summary Table

| Action            | Method                      |
|-------------------|-----------------------------|
| Click             | `click()`                   |
| Type Text         | `sendKeys("text")`         |
| Clear Text        | `clear()`                   |
| Get Text          | `getText()`                 |
| Get Attribute     | `getAttribute("name")`     |
| Is Displayed      | `isDisplayed()`             |
| Is Enabled        | `isEnabled()`               |
| Is Selected       | `isSelected()`              |
| Submit Form       | `submit()`                  |

