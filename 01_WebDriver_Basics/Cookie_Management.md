# Cookie_Management

This document provides a **comprehensive guide** on managing cookies in Selenium WebDriver.

---

## What Are Cookies?

Cookies are small text files stored in the browser that hold user data like:
- Session tokens
- Authentication info
- User preferences

In test automation, interacting with cookies allows you to control the browser session, simulate logged-in states, and validate cookie-dependent features.

---

## 1. Adding Cookies

You can programmatically **add a cookie** to the browser session.

```java
import org.openqa.selenium.Cookie;

// Create a cookie
Cookie cookie = new Cookie("sessionToken", "abc123");

// Add cookie to browser
driver.manage().addCookie(cookie);
```

- **Name**: Identifier of the cookie.
- **Value**: Data associated with the cookie.
- **Domain/Path/Expiry**: Optional parameters.

---

## 2. Reading Cookies

### Get All Cookies

```java
Set<Cookie> cookies = driver.manage().getCookies();
for (Cookie c : cookies) {
    System.out.println(c.getName() + ": " + c.getValue());
}
```

### Get a Specific Cookie

```java
Cookie cookie = driver.manage().getCookieNamed("sessionToken");
System.out.println(cookie.getValue());
```

---

## 3. Deleting Cookies

### Delete a Specific Cookie

```java
driver.manage().deleteCookieNamed("sessionToken");
```

### Delete All Cookies

```java
driver.manage().deleteAllCookies();
```

---

## Use Cases

- **Skipping Login**: Inject session cookies to bypass login screens.
- **State Management**: Set app state without UI interaction.
- **Negative Testing**: Test behavior when cookies are missing or corrupted.

---

## Best Practices

- Always check domain and path to ensure correct cookie scope.
- Be cautious when deleting cookies—some are critical for site functionality.
- Validate cookie addition by reading back and asserting its presence.
