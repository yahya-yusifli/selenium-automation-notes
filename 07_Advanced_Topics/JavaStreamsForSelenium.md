# Java Streams for Selenium (Detailed and Practical Usage)


## Why Are Java Streams Useful in Selenium?

- Easily process lists of WebElements (like search results, dropdown items, tables).
- Reduce boilerplate loops.
- Apply filtering, mapping, grouping, and matching operations concisely.
- Improve readability and maintainability.

---

## Common and Detailed Use Cases

### 1. Extract All Element Texts

```java
List<WebElement> elements = driver.findElements(By.cssSelector("ul li"));
List<String> texts = elements.stream()
    .map(WebElement::getText)
    .collect(Collectors.toList());
```

**Use Case:** Get all item names from a list or dropdown.

### Example Output:
```
["Apple", "Banana", "Cherry"]
```

---

### 2. Check If a Specific Text Exists

```java
boolean hasProduct = elements.stream()
    .anyMatch(e -> e.getText().equalsIgnoreCase("Banana"));
```

**Use Case:** Verify if a specific product or button is present.

### Example Output:
```
true (if "Banana" exists)
```

---

### 3. Filter Elements by Partial Match

```java
List<String> filtered = elements.stream()
    .map(WebElement::getText)
    .filter(text -> text.contains("Pro"))
    .collect(Collectors.toList());
```

**Use Case:** Get all product names containing "Pro".

### Example Output:
```
["MacBook Pro", "iPad Pro"]
```

---

### 4. Count Elements Matching a Condition

```java
long count = elements.stream()
    .filter(e -> e.getText().startsWith("A"))
    .count();
```

**Use Case:** Count how many items start with the letter "A".

### Example Output:
```
2 (if "Apple" and "AirPods")
```

---

### 5. Sort and Collect Element Texts

```java
List<String> sorted = elements.stream()
    .map(WebElement::getText)
    .sorted()
    .collect(Collectors.toList());
```

**Use Case:** Sort product names alphabetically.

### Example Output:
```
["AirPods", "Apple", "iPhone"]
```

---

### 6. Find the First Matching Element

```java
Optional<String> first = elements.stream()
    .map(WebElement::getText)
    .filter(text -> text.endsWith("Pro"))
    .findFirst();

if (first.isPresent()) {
    System.out.println("First matching item: " + first.get());
}
```

**Use Case:** Get the first product ending with "Pro".

### Example Output:
```
First matching item: MacBook Pro
```

---

### 7. Click the First Matching Element

```java
Optional<WebElement> match = elements.stream()
    .filter(e -> e.getText().equals("Checkout"))
    .findFirst();

match.ifPresent(WebElement::click);
```

**Use Case:** Find and click the "Checkout" button from a list.

---

### 8. Join All Texts into a Single String

```java
String joined = elements.stream()
    .map(WebElement::getText)
    .collect(Collectors.joining(", "));
```

**Use Case:** Create a comma-separated list of all item names.

### Example Output:
```
"Apple, Banana, Cherry"
```

---

## Best Practices for Using Streams in Selenium

- **Avoid modifying the DOM inside streams.** Use streams only for read operations (filtering, collecting, counting).
- **Be cautious with large lists.** Streams process efficiently but don’t replace good locator strategies.
- **Combine streams with proper waits.** Ensure elements are loaded before collecting them.
- **Use Optional wisely.** Always check `.isPresent()` before using `.get()` to avoid `NoSuchElementException`.

---

## Summary

Java Streams are a powerful addition to Selenium test code when used correctly. They:
- Simplify collection processing.
- Enable concise filtering, mapping, and matching.
- Improve readability for list-heavy page components.

