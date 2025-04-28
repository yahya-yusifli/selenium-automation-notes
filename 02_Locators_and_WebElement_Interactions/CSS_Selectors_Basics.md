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
