# CSS Selectors Basics

- CSS Selectors are faster and more flexible than XPath.
- Used for locating elements by id, class, attributes, etc.

---

### 1. Select by Class

```java
driver.findElement(By.cssSelector(".className"));
```
- Starts with a `.` → Example: `.submitBtn`

---

### 2. Select by ID

```java
driver.findElement(By.cssSelector("#idName"));
```
- Starts with a `#` → Example: `#username`

---

### 3. Select by Tag Name

```java
driver.findElement(By.cssSelector("tagName"));
```
- Example: `input`, `button`

---

### 4. Select by Attribute

```java
driver.findElement(By.cssSelector("tagName[attribute='value']"));
```
- Example: `input[placeholder='Email']`

---

### 5. Select by Tag Name + Class

```java
driver.findElement(By.cssSelector("tagName.className"));
```
- Example: `button.submitBtn`

---

### 6. Select by Tag Name + ID

```java
driver.findElement(By.cssSelector("tagName#idName"));
```
- Example: `input#username`

---

### 7. Select by Partial Attribute (* contains)

```java
driver.findElement(By.cssSelector("tagName[attribute*='partialValue']"));
```
- Example: `input[placeholder*='mail']`

---

### 8. Select Child Element (Parent > Child)

```java
driver.findElement(By.cssSelector("parentTag > childTag"));
```
- `>` selects only **direct child**.  
- Example: `form > input`

---

### 9. Select by nth-child()

```java
driver.findElement(By.cssSelector("tagName:nth-child(n)"));
```
- Example: `input:nth-child(3)`

---

### 10. Select by Multiple Attributes

```java
driver.findElement(By.cssSelector("tagName[attribute1='value'][attribute2='value']"));
```
- Example: `input[type='text'][placeholder='Name']`

---

### 11. Descendant Selection (Space between tags)

```java
driver.findElement(By.cssSelector("parentTag descendantTag"));
```
- Example: `div input`


---


# CSS Attribute Matching Operators ( Regular expression )


| Operator | Meaning | Syntax Example | Matches Example |
|:---|:---|:---|:---|
| `=` | Exact match | `input[type='text']` | Matches `<input type="text">` |
| `*=` | Contains match | `input[placeholder*='name']` | Matches `<input placeholder="Enter your name">` |
| `^=` | Starts with match | `input[placeholder^='Enter']` | Matches `<input placeholder="Enter your name">` |
| `$=` | Ends with match | `input[placeholder$='name']` | Matches `<input placeholder="Enter your name">` |

---

### 1. Exact Match (`=`)

- **Selector:**  
  ```java
  driver.findElement(By.cssSelector("input[type='text']"));
  ```
- **HTML Example:**
  ```html
  <input type="text">
  ```
- **Meaning:**  
  Selects `<input>` where `type` is exactly `"text"`.

---

### 2. Contains Match (`*=`)

- **Selector:**  
  ```java
  driver.findElement(By.cssSelector("input[placeholder*='name']"));
  ```
- **HTML Example:**
  ```html
  <input placeholder="Enter your name">
  ```
- **Meaning:**  
  Selects `<input>` where `placeholder` **contains** `"name"`.

---

### 3. Starts With Match (`^=`)

- **Selector:**  
  ```java
  driver.findElement(By.cssSelector("input[placeholder^='Enter']"));
  ```
- **HTML Example:**
  ```html
  <input placeholder="Enter your name">
  ```
- **Meaning:**  
  Selects `<input>` where `placeholder` **starts with** `"Enter"`.

---

### 4. Ends With Match (`$=`)

- **Selector:**  
  ```java
  driver.findElement(By.cssSelector("input[placeholder$='name']"));
  ```
- **HTML Example:**
  ```html
  <input placeholder="Enter your name">
  ```
- **Meaning:**  
  Selects `<input>` where `placeholder` **ends with** `"name"`.

---


### Tip

- Use `*=` when IDs, classes, or names are **partially dynamic**.
- Use `^=` or `$=` when only **start or end of attribute** is predictable.

---


---
