# Dynamic Locators in Selenium

Dynamic locators are strategies used to handle elements whose attributes or positions change frequently between page loads or user sessions.

They help you write robust and resilient test scripts that don’t break when minor UI or HTML changes occur.

---

## Why Do We Need Dynamic Locators?

- Many modern web applications generate elements with dynamic IDs or classes (e.g., `id="user_123"`, where `123` changes).  
- Hardcoding static locators (like exact IDs or full XPath paths) will fail when those change.  
- Dynamic locators allow you to adapt to such changes by focusing on stable parts of the element.

---

## Common Strategies

### 1. Using Contains in XPath

```java
driver.findElement(By.xpath("//tag[contains(@attribute,'partialValue')]"));
```

Example:
```java
driver.findElement(By.xpath("//input[contains(@id,'username')]"));
```

HTML Example:
```html
<input id="user_123" type="text">
```

---

### 2. Using Starts-With in XPath

```java
driver.findElement(By.xpath("//tag[starts-with(@attribute,'startValue')]"));
```

Example:
```java
driver.findElement(By.xpath("//div[starts-with(@id,'message_')]"));
```

HTML Example:
```html
<div id="message_456">Welcome!</div>
```

---

### 3. Using Ends-With (CSS Only, no XPath)

```java
driver.findElement(By.cssSelector("tag[attribute$='endValue']"));
```

Example:
```java
driver.findElement(By.cssSelector("input[id$='_input']"));
```

HTML Example:
```html
<input id="username_input" type="text">
```

---

### 4. Using Attribute Contains in CSS

```java
driver.findElement(By.cssSelector("tag[attribute*='partialValue']"));
```

Example:
```java
driver.findElement(By.cssSelector("button[class*='submit']"));
```

HTML Example:
```html
<button class="btn submit-btn">Submit</button>
```

---

### 5. Using Dynamic Indexing

If multiple matching elements exist, but you always want, for example, the first one:

```java
driver.findElement(By.xpath("(//tag[contains(@attribute,'partialValue')])[1]"));
```
Example:
```html
<div class="item-list">
    <button class="delete-btn">Delete Item 1</button>
    <button class="delete-btn">Delete Item 2</button>
    <button class="delete-btn">Delete Item 3</button>
</div>
```
```java
driver.findElement(By.xpath("(//button[contains(@class,'delete')])[1]"));
```

---

## Tips for Building Robust Dynamic Locators

- Avoid brittle locators: Don’t rely on full XPaths that depend on exact tree position.  
- Look for stable attributes: Like labels, placeholders, aria-labels, or data-* attributes.  
- Combine multiple attributes: For better precision, e.g., `//input[@type='text' and contains(@id,'user')]`.  
- Ask developers: Sometimes they can add `data-testid` or `data-qa` attributes just for testing.

---

## Summary Table

| Strategy                  | Example Syntax                                     |
|---------------------------|---------------------------------------------------|
| XPath contains            | `//input[contains(@id,'user')]`                   |
| XPath starts-with         | `//div[starts-with(@id,'msg_')]`                  |
| CSS ends-with            | `input[id$='_input']`                             |
| CSS contains             | `button[class*='submit']`                         |
| XPath with index         | `(//button[contains(@class,'delete')])[1]`        |

If you want, I can prepare a helper utility class or reusable methods for dynamic locators. Let me know!
