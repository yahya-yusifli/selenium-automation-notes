## Implicit Wait

Implicit wait tells WebDriver to poll the DOM for a certain amount of time when trying to find any element.

---

### Pros
- Simple to implement (one-line setup)
- Automatically applies to all element searches
- Reduces the chance of `NoSuchElementException` for slow-loading elements

### Cons
- Cannot handle specific element conditions (like visibility or clickability)
- Applies globally, which may slow down tests unnecessarily if overused
- Cannot combine well with explicit waits (can cause unexpected delays or timeouts)
- Harder to debug when failures occur because wait is hidden in the background

---

### Example

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
```

### Key Points
- Applies globally to all `findElement` or `findElements`
- Once set, it lasts for the entire WebDriver session
- Limitation: cannot target specific elements or conditions
