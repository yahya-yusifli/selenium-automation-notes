## Explicit Wait (WebDriverWait)

Explicit wait allows waiting for a specific condition before proceeding.

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

- Targets a specific element or condition
- More flexible than implicit wait
- Can wait for visibility, clickability, presence, etc.

---
