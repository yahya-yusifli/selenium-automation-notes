# XPath Sibling Traversal

## 1. Following-Sibling Traversal

Selects all sibling elements that come **after** the current node.

### Syntax
```java
driver.findElement(By.xpath("//tag[@attribute='value']/following-sibling::siblingTag"));
```

### Example
```java
driver.findElement(By.xpath("//label[@for='email']/following-sibling::input"));
```

**HTML Example:**
```html
<label for="email">Email</label>
<input type="email" id="email">
```
This XPath selects the `<input>` element that comes after the `<label>`.

---

## 2. Preceding-Sibling Traversal

Selects all sibling elements that come **before** the current node.

### Syntax
```java
driver.findElement(By.xpath("//tag[@attribute='value']/preceding-sibling::siblingTag"));
```

### Example
```java
driver.findElement(By.xpath("//input[@id='email']/preceding-sibling::label"));
```

**HTML Example:**
```html
<label for="email">Email</label>
<input type="email" id="email">
```
This XPath selects the `<label>` element that comes before the `<input>`.

---

## 3. Select Specific Sibling by Index

When multiple siblings match, you can use indexing.

### Syntax
```java
driver.findElement(By.xpath("//tag/following-sibling::siblingTag[n]"));
```

### Example
```java
driver.findElement(By.xpath("//button[1]/following-sibling::button[2]"));
```

**HTML Example:**
```html
<div>
    <button id="btn1">First</button>
    <button id="btn2">Second</button>
    <button id="btn3">Third</button>
</div>
```
This XPath selects the third button (second following sibling after the first).

---

## Summary Table

| Traversal Type        | Syntax Example                                      | Use Case                                     |
|-----------------------|-----------------------------------------------------|---------------------------------------------|
| Following sibling     | `//label[@for='email']/following-sibling::input`    | Select element after the current element    |
| Preceding sibling     | `//input[@id='email']/preceding-sibling::label`     | Select element before the current element   |
| Sibling by index      | `//button[1]/following-sibling::button[2]`          | Select specific sibling by position         |

