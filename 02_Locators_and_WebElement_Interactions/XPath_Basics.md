# XPath Basics

- XPath is used to navigate through elements and attributes.
- It supports complex and dynamic element identification.

### Examples:
```java
driver.findElement(By.xpath("//input[@id='username']")).sendKeys("testUser");
driver.findElement(By.xpath("//button[text()='Sign In']")).click();
```

---

## Using XPath to Locate the Third Input Inside a Form

**Code Example:**
```java
driver.findElement(By.xpath("//form/input[3]")).sendKeys("exampleText");
```

---

## Explanation:

- `//form`:
  ➔ Selects any `<form>` element in the page.

- `/input[3]`:
  ➔ From that `<form>`, selects the **third `<input>` child**.

- `sendKeys("exampleText")`:
  ➔ Types `"exampleText"` into the selected third input field.

---

## Example HTML Structure:

```html
<form action="#">
    <h2>Forgot password</h2>
    <input type="text" placeholder="Name" style="">
    <input type="text" placeholder="Email" style="">
    <input type="text" placeholder="Phone Number" style="" xpath="1">
    <br>
    <div class="forgot-pwd-btn-conainer">
        <button class="go-to-login-btn">Go to Login</button>
        <button class="reset-pwd-btn">Reset Login</button>
    </div>
</form>
```

- In this structure:
  - First child: `<h2>` (not an input)
  - Second child: `<input placeholder="Name">`
  - Third child: `<input placeholder="Email">`
  - Fourth child: `<input placeholder="Phone Number">`
  
**Important:**  
XPath `/input[3]` looks only at `<input>` elements, **not other tags** like `<h2>`, `<br>`, or `<div>`.

So,  
- `//form/input[3]` will select the `<input>` field for **Phone Number**.

---

## Alternative (More Reliable) XPath:

If you want to make sure you select the third input based only on inputs (ignoring non-input tags):

```java
driver.findElement(By.xpath("(//form//input)[3]")).sendKeys("exampleText");
```

- `(//form//input)[3]` ➔ Selects the third `<input>` anywhere inside the form, ignoring other elements.

---

## Real-World Tip:

- **Be careful when using child indexing** if the form contains other elements like `<h2>`, `<div>`, `<br>`, etc.
- Safer XPath usually uses double slashes `//input` inside the form instead of relying strictly on `/input[n]`.

---

