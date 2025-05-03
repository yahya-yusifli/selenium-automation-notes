## Fluent Wait in Selenium

Fluent Wait is an advanced form of explicit wait that:
Fluent Wait is a Selenium wait that repeatedly checks for a condition at defined time intervals, ignoring specified exceptions, until a maximum timeout is reached.

* Defines polling intervals (how often to check)
* Ignores specific exceptions during waiting
* Gives fine control over the wait process
  
---

### Example Usage

```java
Wait<WebDriver> fluentWait = new FluentWait<>(driver)
    .withTimeout(Duration.ofSeconds(30))
    .pollingEvery(Duration.ofSeconds(5))
    .ignoring(NoSuchElementException.class);

fluentWait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

This waits up to **30 seconds**, checking every **5 seconds**, ignoring `NoSuchElementException` until the condition is met.

---

### Pros

* Custom polling intervals for better performance
* Can ignore specific exceptions (e.g., element not found)
* More flexible than standard explicit waits
* Reduces unnecessary checks compared to fixed waits

---

### Cons

* Slightly more complex to implement
* Overuse can make code harder to maintain
* Needs careful tuning to avoid too long or too short polling
* Still depends on correct ExpectedConditions

---

### Difference from WebDriverWait

WebDriverWait is a simplified form of Fluent Wait with default polling (500ms) and no custom exception handling, making it easier but less flexible.

---
### When to Use

* On elements that appear unpredictably (not just after page load)
* When dealing with flaky elements or AJAX-heavy apps
* To replace or improve upon hard-coded waits like `Thread.sleep()`

---

