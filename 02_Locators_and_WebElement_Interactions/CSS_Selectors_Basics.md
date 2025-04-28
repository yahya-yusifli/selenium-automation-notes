# CSS Selectors Basics

- CSS Selectors are faster and more flexible than XPath.
- Used for locating elements by id, class, attributes, etc.

### Examples:
```java
driver.findElement(By.cssSelector("input[placeholder='Email']")).sendKeys("test@email.com");
driver.findElement(By.cssSelector(".submitBtn")).click();
driver.findElement(By.cssSelector("#username")).sendKeys("myUser");

```

---

## Using CSS Selector with nth-child to Locate an Element

**Code Example:**
```java
driver.findElement(By.cssSelector("input[type='text']:nth-child(3)")).sendKeys("user3@email.com");
```

---

## Explanation:

- `input[type='text']`:  
  ➔ Selects all `<input>` elements where the `type` attribute equals `"text"`.

- `:nth-child(3)`:  
  ➔ Picks the **third child element** (relative to its parent) among **all siblings**.

- `sendKeys("user3@email.com")`:  
  ➔ Types the text `"user3@email.com"` into the selected input field.

---

## Important Note:

- `nth-child()` counts the **position among all siblings**, not just inputs.
- If the parent element has other tags like `<label>`, `<div>`, they will be counted too.
- This method is **sensitive to page structure changes**.
  - If the HTML changes (elements added/removed), `nth-child(3)` might no longer point to the intended input field.

---

## Example HTML Structure:

```html
<div class="form-container">
    <input type="text" placeholder="Name">
    <input type="text" placeholder="Email">
    <input type="text" placeholder="Phone">
</div>
```

- In this case, `:nth-child(3)` would select the third child — the **Phone** input field.

---

## Alternative (Safer) Option Using XPath

If you want to **directly target** the third `input` element where `type='text'`,  
regardless of sibling positions, XPath is safer:

```java
driver.findElement(By.xpath("(//input[@type='text'])[3]")).sendKeys("user3@email.com");
```

- `(//input[@type='text'])[3]` counts only matching `input` elements, **ignoring other tags**.

---
