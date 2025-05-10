# XPath Contains and Starts-With

`contains()` and `starts-with()` functions in XPath to create flexible and reliable locators for Selenium automation.

---

## 1. Using contains() in XPath

The `contains()` function helps locate elements where an attribute or text **partially matches** a value.

### Syntax
```java
driver.findElement(By.xpath("//tag[contains(@attribute, 'partialValue')]");
```

### Example 1: Attribute Contains
```java
driver.findElement(By.xpath("//input[contains(@id, 'user')]");
```

**HTML Example:**
```html
<input id="username" type="text">
<input id="userEmail" type="email">
```
This XPath matches both inputs because their `id` contains "user".

### Example 2: Text Contains
```java
driver.findElement(By.xpath("//button[contains(text(), 'Log')]");
```

**HTML Example:**
```html
<button>Login</button>
<button>Logout</button>
```
This XPath matches both buttons because their text contains "Log".

---

## 2. Using starts-with() in XPath

The `starts-with()` function helps locate elements where an attribute **starts with** a specific value.

### Syntax
```java
driver.findElement(By.xpath("//tag[starts-with(@attribute, 'startValue')]");
```

### Example 1: Attribute Starts With
```java
driver.findElement(By.xpath("//div[starts-with(@id, 'message_')]");
```

**HTML Example:**
```html
<div id="message_1">Hello</div>
<div id="message_2">World</div>
```
This XPath matches both `<div>` elements because their `id` starts with "message_".

### Example 2: Text Starts With
```java
driver.findElement(By.xpath("//p[starts-with(text(), 'Welcome')]");
```

**HTML Example:**
```html
<p>Welcome to the site!</p>
```
This XPath matches the `<p>` element because its text starts with "Welcome".

---

## Summary Table

| Function        | Purpose                         | Example Syntax                                     |
|-----------------|---------------------------------|---------------------------------------------------|
| contains()      | Partial match in attribute/text | `//input[contains(@id,'user')]`                   |
| starts-with()   | Starts-with match in attribute/text | `//div[starts-with(@id,'msg_')]`                  |

If you want, I can also include examples using `contains()` or `starts-with()` combined with other XPath functions for more advanced targeting. Let me know!
