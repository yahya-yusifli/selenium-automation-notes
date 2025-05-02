
## Implicit Wait

Implicit wait tells WebDriver to poll the DOM for a certain amount of time when trying to find any element.

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
```

- Applies globally to all `findElement` or `findElements`
- Once set, it lasts for the entire session
- **Limitation:** cannot target specific elements or conditions

---
