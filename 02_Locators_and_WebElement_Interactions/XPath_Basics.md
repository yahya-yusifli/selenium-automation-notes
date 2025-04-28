# XPath Basics

- XPath is used to navigate through elements and attributes.
- It supports complex and dynamic element identification.

### Examples:
```java
driver.findElement(By.xpath("//input[@id='username']")).sendKeys("testUser");
driver.findElement(By.xpath("//button[text()='Sign In']")).click();
```
---

## Selecting the Nth Child Element Using XPath

---

### Code Example

```java
driver.findElement(By.xpath("//form/input[3]")).sendKeys("exampleText");
```

---

### Small HTML Example

```html
<form>
    <input type="text" placeholder="Name">
    <input type="text" placeholder="Email">
    <input type="text" placeholder="Phone Number">
</form>
```
- 1st input ➔ Name
- 2nd input ➔ Email
- 3rd input ➔ Phone Number

`//form/input[3]` will select **Phone Number** field.

---

### Important Points

- `//form/input[3]` ➔ Selects the **third direct `<input>`** under `<form>`.
- Only **direct children** are counted.
- **If page structure changes**, this XPath may fail.

---

### Safer Alternative

```java
driver.findElement(By.xpath("(//form//input)[3]")).sendKeys("exampleText");
```
- `(//form//input)[3]` ➔ Selects the **third input** anywhere inside the form, even if deeply nested.

---
