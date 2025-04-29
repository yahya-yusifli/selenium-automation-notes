# TestNG Assertions

TestNG provides a set of assertion methods to validate actual outcomes against expected results in test automation. These are essential for verifying the correctness of your tests.

---

## 1. `assertEquals(actual, expected)`

Checks whether two values are equal. If not, the test fails.

```java
Assert.assertEquals(driver.getTitle(), "Home Page");
```

 **Use When:**
- Verifying page title, element text, or returned values

---

## 2. `assertTrue(condition)`

Asserts that a condition is true.

```java
Assert.assertTrue(driver.findElement(By.id("logoutBtn")).isDisplayed());
```

 **Use When:**
- Checking element visibility
- Validating that a condition is met

---

## 3. `assertFalse(condition)`

Asserts that a condition is false.

```java
Assert.assertFalse(driver.findElement(By.id("errorMsg")).isDisplayed());
```

 **Use When:**
- Confirming error or unwanted elements are not present

---

## 4. `assertNotEquals(actual, unexpected)`

Fails if the actual value equals the unexpected one.

```java
Assert.assertNotEquals(actualStatus, "FAILED");
```

 **Use When:**
- Ensuring unexpected values are not returned

---

## 5. `assertNull(object)`

Asserts that the object is null.

```java
Assert.assertNull(driver.findElement(By.id("unknown")));
```

 **Use When:**
- Validating that a value was not initialized or returned

---

## 6. `assertNotNull(object)`

Asserts that the object is not null.

```java
Assert.assertNotNull(driver.findElement(By.id("loginBtn")));
```

 **Use When:**
- Confirming an element or object is present

---

## 7. Verifying Text with `getText()` and `assertEquals()`

```java
Assert.assertEquals(
    driver.findElement(By.tagName("p")).getText(),
    "You are successfully logged in."
);
```

🔍 **Explanation:**
- `getText()` extracts visible string from an element.
- `assertEquals()` compares actual text with expected text.
- Used in post-login, submission confirmations, success/error messages.

---

## Summary Table

| Method | Description |
|--------|-------------|
| `assertEquals(a, b)` | Passes if `a == b` |
| `assertTrue(cond)` | Passes if condition is true |
| `assertFalse(cond)` | Passes if condition is false |
| `assertNotEquals(a, b)` | Passes if `a != b` |
| `assertNull(obj)` | Passes if object is null |
| `assertNotNull(obj)` | Passes if object is not null |

---

## ✅ Best Practices

- Always include a message in assertions for better test reporting:

```java
Assert.assertEquals(actual, expected, "Login success message mismatch");
```

- Use assertions immediately after the action you want to validate.
- Assertions help you detect issues early and make debugging easier.

---
