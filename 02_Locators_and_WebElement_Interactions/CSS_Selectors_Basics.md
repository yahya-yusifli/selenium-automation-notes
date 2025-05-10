# CSS Selectors Basics

- CSS Selectors are faster and more flexible than XPath.
- Used for locating elements by id, class, attributes, etc.

---

### 1. Select by Class

```java
driver.findElement(By.cssSelector(".className"));
```
- Starts with a `.` → Example: `.submitBtn`

**HTML Example:**
```html
<button class="submitBtn">Submit</button>
```

---

### 2. Select by ID

```java
driver.findElement(By.cssSelector("#idName"));
```
- Starts with a `#` → Example: `#username`

**HTML Example:**
```html
<input id="username" type="text">
```

---

### 3. Select by Tag Name

```java
driver.findElement(By.cssSelector("tagName"));
```
- Example: `input`, `button`

**HTML Example:**
```html
<input type="text">
```

---

### 4. Select by Attribute

```java
driver.findElement(By.cssSelector("tagName[attribute='value']"));
```
- Example: `input[placeholder='Email']`

**HTML Example:**
```html
<input type="text" placeholder="Email">
```

---

### 5. Select by Tag Name + Class

```java
driver.findElement(By.cssSelector("tagName.className"));
```
- Example: `button.submitBtn`

**HTML Example:**
```html
<button class="submitBtn">Submit</button>
```

---

### 6. Select by Tag Name + ID

```java
driver.findElement(By.cssSelector("tagName#idName"));
```
- Example: `input#username`

**HTML Example:**
```html
<input id="username" type="text">
```

---

### 7. Select by Partial Attribute (* contains)

```java
driver.findElement(By.cssSelector("tagName[attribute*='partialValue']"));
```
- Example: `input[placeholder*='mail']`

**HTML Example:**
```html
<input placeholder="Email address">
```

---

### 8. Select Child Element (Parent > Child)

```java
driver.findElement(By.cssSelector("parentTag > childTag"));
```
- `>` selects only **direct child**.  
- Example: `form > input`

**HTML Example:**
```html
<form>
    <input type="text" name="username">
</form>
```

---

### 9. Select by nth-child()

```java
driver.findElement(By.cssSelector("tagName:nth-child(n)"));
```
- Example: `input:nth-child(3)`

**HTML Example:**
```html
<form>
    <input type="text">
    <input type="text">
    <input type="email">
</form>
```

---

### 10. Select by Multiple Attributes

```java
driver.findElement(By.cssSelector("tagName[attribute1='value'][attribute2='value']"));
```
- Example: `input[type='text'][placeholder='Name']`

**HTML Example:**
```html
<input type="text" placeholder="Name">
```

---

### 11. Descendant Selection (Space between tags)

```java
driver.findElement(By.cssSelector("parentTag descendantTag"));
```
- Example: `div input`

**HTML Example:**
```html
<div>
    <input type="text">
</div>
```

---

# CSS Attribute Matching Operators (Regular Expression)

| Operator | Meaning            | Syntax Example                   | Matches Example                              |
|:---------|:-------------------|:---------------------------------|:--------------------------------------------|
| `=`      | Exact match        | `input[type='text']`             | Matches `<input type="text">`              |
| `*=`     | Contains match     | `input[placeholder*='name']`     | Matches `<input placeholder="Enter name">` |
| `^=`     | Starts with match  | `input[placeholder^='Enter']`    | Matches `<input placeholder="Enter name">` |
| `$=`     | Ends with match    | `input[placeholder$='name']`     | Matches `<input placeholder="Enter name">` |

---

### 1. Exact Match (`=`)

```java
driver.findElement(By.cssSelector("input[type='text']"));
```

**HTML Example:**
```html
<input type="text">
```

---

### 2. Contains Match (`*=`)

```java
driver.findElement(By.cssSelector("input[placeholder*='name']"));
```

**HTML Example:**
```html
<input placeholder="Enter your name">
```

---

### 3. Starts With Match (`^=`)

```java
driver.findElement(By.cssSelector("input[placeholder^='Enter']"));
```

**HTML Example:**
```html
<input placeholder="Enter your name">
```

---

### 4. Ends With Match (`$=`)

```java
driver.findElement(By.cssSelector("input[placeholder$='name']"));
```

**HTML Example:**
```html
<input placeholder="Enter your name">
```

---

### Tip

- Use `*=` when IDs, classes, or names are **partially dynamic**.
- Use `^=` or `$=` when only **start or end of attribute** is predictable.
