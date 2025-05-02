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
---
# Explicit Wait Methods in Selenium (WebDriverWait)

This note details the most common explicit wait methods using `ExpectedConditions`, followed by additional less common but useful ones.

---

## Common Methods

### 1. `visibilityOfElementLocated`
Waits until the specified element is present in the DOM and visible (non-zero size, not hidden).

```java
wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

### 2. `presenceOfElementLocated`
Waits until the element is present in the DOM but does not require it to be visible.

```java
wait.until(ExpectedConditions.presenceOfElementLocated(By.id("username")));
```

### 3. `elementToBeClickable`
Waits until the element is visible and enabled, meaning it can be clicked.

```java
wait.until(ExpectedConditions.elementToBeClickable(By.id("submit")));
```

### 4. `invisibilityOfElementLocated`
Waits until the specified element is either not present in the DOM or hidden.

```java
wait.until(ExpectedConditions.invisibilityOfElementLocated(By.id("loading")));
```

### 5. `textToBePresentInElement`
Waits until the given text appears inside the specified element.

```java
wait.until(ExpectedConditions.textToBePresentInElement(By.id("status"), "Success"));
```

### 6. `alertIsPresent`
Waits until a JavaScript alert is present on the page.

```java
wait.until(ExpectedConditions.alertIsPresent());
```

---

## Additional Useful Methods

### `titleIs`
Waits until the page title is exactly the given string.
```java
wait.until(ExpectedConditions.titleIs("Expected Page Title"));
```

### `titleContains`
Waits until the page title contains a given substring.
```java
wait.until(ExpectedConditions.titleContains("Expected Substring"));
```

### `urlToBe`
Waits until the current URL matches the given URL.
```java
wait.until(ExpectedConditions.urlToBe("https://example.com/home"));
```

### `urlContains`
Waits until the current URL contains the given substring.
```java
wait.until(ExpectedConditions.urlContains("/home"));
```

### `frameToBeAvailableAndSwitchToIt`
Waits until the frame is available and automatically switches to it.
```java
wait.until(ExpectedConditions.frameToBeAvailableAndSwitchToIt("frameName"));
```

### `numberOfElementsToBe`
Waits until the number of elements matching the locator equals the expected number.
```java
wait.until(ExpectedConditions.numberOfElementsToBe(By.cssSelector(".items"), 5));
```

### `stalenessOf`
Waits until the given element is no longer attached to the DOM.
```java
wait.until(ExpectedConditions.stalenessOf(oldElement));
```

### `elementSelectionStateToBe`
Waits until the element’s selection state matches the expected state (checked/unchecked).
```java
wait.until(ExpectedConditions.elementSelectionStateToBe(checkbox, true));
```

---

## Summary
- Use common methods for general interactions (visibility, clickability, presence).
- Use additional methods for page state, URL, title, frame, or advanced conditions.
- Always pick the condition that precisely matches your use case for reliable and efficient waits.
