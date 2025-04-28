# XPath Basics

- XPath is used to navigate through elements and attributes.
- It supports complex and dynamic element identification.

### Examples:
```java
driver.findElement(By.xpath("//input[@id='username']")).sendKeys("testUser");
driver.findElement(By.xpath("//button[text()='Sign In']")).click();
```
---

# Selecting the Nth Child Element Using XPath
### Code Example

```java
driver.findElement(By.xpath("//form/input[3]")).sendKeys("exampleText");
```

- `//form` ➔ Find any `<form>`.
- `/input[3]` ➔ Select the third `<input>` child.
- `sendKeys()` ➔ Type text inside the input.

---

### Example HTML

```html
<form>
    <h2>Forgot password</h2>
    <input type="text" placeholder="Name">
    <input type="text" placeholder="Email">
    <input type="text" placeholder="Phone Number">
</form>
```

- 1st child: `<h2>` (ignored)
- 2nd input: Name
- 3rd input: Email
- 4th input: Phone Number

 `//form/input[3]` selects **Phone Number input**.

---

### Important

- `/input[3]` counts **only direct input children**.
- Other tags like `<h2>`, `<div>` can break the count.
- If page structure changes, locator may fail.

---

### Safer Option

```java
driver.findElement(By.xpath("(//form//input)[3]")).sendKeys("exampleText");
```
- `(//form//input)[3]` ➔ Selects third `<input>` anywhere inside form.
- Ignores other tags.

---

