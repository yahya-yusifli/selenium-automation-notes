# CSS Selectors Basics

- CSS Selectors are faster and more flexible than XPath.
- Used for locating elements by id, class, attributes, etc.
---

| Selector Type        | Syntax                       | Description                                                           | Java Example                                                             |
|----------------------|------------------------------|-----------------------------------------------------------------------|---------------------------------------------------------------------------|
| Universal            | `*`                          | Matches **any** element                                                | `driver.findElement(By.cssSelector("*"));`                                |
| Element              | `tag`                        | Matches all elements with the given tag name                           | `driver.findElement(By.cssSelector("input"));`                            |
| ID                   | `#id`                        | Matches the element whose `id` attribute equals `id`                   | `driver.findElement(By.cssSelector("#username"));`                        |
| Class                | `.class`                     | Matches all elements with the specified class                          | `driver.findElement(By.cssSelector(".submitBtn"));`                       |
| Multiple Classes     | `.c1.c2`                     | Matches elements that have **both** classes `c1` and `c2`              | `driver.findElement(By.cssSelector("button.btn.primary"));`               |
| Tag + Class          | `tag.class`                  | Matches elements of the given tag **and** class                        | `driver.findElement(By.cssSelector("button.primary"));`                   |
| Tag + ID             | `tag#id`                     | Matches elements of the given tag with the specified `id`              | `driver.findElement(By.cssSelector("input#searchBox"));`                  |
| Grouping             | `sel1, sel2`                 | Matches elements that match **either** selector                        | `driver.findElement(By.cssSelector("button.primary, a.link"));`           |
| Attribute Equals     | `[attr='value']`             | Matches elements whose `attr` value **exactly** equals `value`         | `driver.findElement(By.cssSelector("input[type='email']"));`              |
| Attribute Contains   | `[attr*='sub']`              | Matches elements whose `attr` value **contains** the substring `sub`   | `driver.findElement(By.cssSelector("input[placeholder*='Email']"));`      |
| Attribute Starts With| `[attr^='start']`            | Matches elements whose `attr` value **starts with** `start`            | `driver.findElement(By.cssSelector("a[href^='https']"));`                 |
| Attribute Ends With  | `[attr$='end']`              | Matches elements whose `attr` value **ends with** `end`                | `driver.findElement(By.cssSelector("img[src$='.png']"));`                 |
| Multiple Attributes  | `tag[a='v1'][b='v2']`        | Matches elements of `tag` satisfying **all** attribute filters         | `driver.findElement(By.cssSelector("input[type='text'][name='user']"));` |
| Descendant           | `ancestor descendant`        | Matches any `descendant` (at any depth) of `ancestor`                  | `driver.findElement(By.cssSelector("div.form-group input"));`             |
| Child                | `parent > child`             | Matches **only** direct `child` elements of `parent`                   | `driver.findElement(By.cssSelector("ul > li"));`                          |
| Adjacent Sibling     | `prev + next`                | Matches a `next` element immediately following `prev`                  | `driver.findElement(By.cssSelector("label + input"));`                    |
| General Sibling      | `prev ~ siblings`            | Matches **all** `siblings` that follow `prev` (not necessarily direct) | `driver.findElement(By.cssSelector("h2 ~ p"));`                           |
| First-Child          | `:first-child`               | Matches elements that are the **first** child of their parent          | `driver.findElement(By.cssSelector("ul li:first-child"));`                |
| Last-Child           | `:last-child`                | Matches elements that are the **last** child of their parent           | `driver.findElement(By.cssSelector("ul li:last-child"));`                 |
| Nth-Child            | `:nth-child(n)`              | Matches the **nᵗʰ** child element (1-based) of its parent               | `driver.findElement(By.cssSelector("tr:nth-child(odd)"));`                |
| Nth-of-Type          | `:nth-of-type(n)`            | Matches the **nᵗʰ** element of its **type** among siblings              | `driver.findElement(By.cssSelector("p:nth-of-type(2)"));`                 |
| Not                  | `:not(selector)`             | Excludes any element matching the inner `selector`                     | `driver.findElement(By.cssSelector("input:not([type='submit'])"));`       |


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
