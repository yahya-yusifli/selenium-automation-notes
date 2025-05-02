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

This note details the most common explicit wait methods using `ExpectedConditions`.

---

## 1. `visibilityOfElementLocated`
Waits until the specified element is present in the DOM and visible (non-zero size, not hidden).

```java
wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

Use when: The element exists but may not yet be visible.

---

## 2. `presenceOfElementLocated`
Waits until the element is present in the DOM but **does not require** it to be visible.

```java
wait.until(ExpectedConditions.presenceOfElementLocated(By.id("username")));
```

Use when: You only need the element loaded, regardless of its visibility.

---

## 3. `elementToBeClickable`
Waits until the element is visible and enabled, meaning it can be clicked.

```java
wait.until(ExpectedConditions.elementToBeClickable(By.id("submit")));
```

Use when: You want to interact with (click) the element safely.

---

## 4. `invisibilityOfElementLocated`
Waits until the specified element is either not present in the DOM or hidden.

```java
wait.until(ExpectedConditions.invisibilityOfElementLocated(By.id("loading")));
```

Use when: You want to wait for a loading spinner or modal to disappear.

---

## 5. `textToBePresentInElement`
Waits until the given text appears inside the specified element.

```java
wait.until(ExpectedConditions.textToBePresentInElement(By.id("status"), "Success"));
```

Use when: You are waiting for dynamic status or label updates.

---

## 6. `alertIsPresent`
Waits until a JavaScript alert is present on the page.

```java
wait.until(ExpectedConditions.alertIsPresent());
```

Use when: You need to handle alerts (accept, dismiss, get text).

---

## Summary
- Always choose the condition that matches your use case.
- Explicit waits provide better reliability for dynamic or AJAX-heavy pages.
- Avoid mixing implicit waits and explicit waits to prevent unexpected behaviors.
