## Fluent Wait

Fluent wait is an advanced form of explicit wait that:
- Defines polling intervals
- Ignores specific exceptions
- Provides fine control over how often conditions are checked

```java
Wait<WebDriver> fluentWait = new FluentWait<>(driver)
    .withTimeout(Duration.ofSeconds(30))
    .pollingEvery(Duration.ofSeconds(5))
    .ignoring(NoSuchElementException.class);

fluentWait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

---

