## Explicit Wait (WebDriverWait)

Explicit wait allows waiting for a specific condition before proceeding.

---

### Pros
- Targets a specific element or condition
- More flexible and precise compared to implicit wait
- Can handle advanced conditions like visibility, clickability, presence, or alert presence
- Reduces unnecessary waiting time compared to global waits
- Improves test reliability when working with dynamic or AJAX-loaded elements

### Cons
- Requires writing extra code for each specific wait
- If overused, can increase code complexity
- Needs careful handling to avoid `TimeoutException`
- Should not be mixed with implicit wait, as this can cause unexpected delays or failures

---

### Example

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

### Key Points
- Waits only for the defined element or condition
- Can be used for visibility, clickability, text presence, URL change, alert presence, etc.
- Requires `ExpectedConditions` helper methods
- Best used when combined carefully within well-structured test flows
