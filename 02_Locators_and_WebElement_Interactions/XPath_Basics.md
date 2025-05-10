# XPath Basics

- XPath is used to navigate through elements and attributes.
- It supports complex and dynamic element identification.

---

### 1. Select by Tag Name

```java
driver.findElement(By.xpath("//tagName"));
```
- Example: `//input`

**HTML Example:**
```html
<input type="text" name="username">
```

---

### 2. Select by Attribute

```java
driver.findElement(By.xpath("//tagName[@attribute='value']"));
```
- Example: `//input[@id='username']`

**HTML Example:**
```html
<input id="username" type="text" name="username">
```

---

### 3. Select by Multiple Attributes

```java
driver.findElement(By.xpath("//tagName[@attribute1='value' and @attribute2='value']"));
```
- Example: `//input[@type='text' and @placeholder='Email']`

**HTML Example:**
```html
<input type="text" placeholder="Email" name="email">
```

---

### 4. Select by Text Content

```java
driver.findElement(By.xpath("//tagName[text()='Exact Text']"));
```
- Example: `//button[text()='Login']`

**HTML Example:**
```html
<button>Login</button>
```

---

### 5. Select by Partial Text (contains)

```java
driver.findElement(By.xpath("//tagName[contains(text(),'PartialText')]"));
```
- Example: `//button[contains(text(),'Log')]`

**HTML Example:**
```html
<button>Log In</button>
```

---

### 6. Select by Attribute Contains

```java
driver.findElement(By.xpath("//tagName[contains(@attribute,'partialValue')]"));
```
- Example: `//input[contains(@placeholder,'mail')]`

**HTML Example:**
```html
<input type="text" placeholder="Email address">
```

---

### 7. Select by Attribute Starts-With

```java
driver.findElement(By.xpath("//tagName[starts-with(@attribute,'valueStart')]"));
```
- Example: `//input[starts-with(@id,'user')]`

**HTML Example:**
```html
<input id="userNameField" type="text">
```

---

### 8. Parent to Child Selection

```java
driver.findElement(By.xpath("//parentTag/childTag"));
```
- Example: `//form/input`

**HTML Example:**
```html
<form>
    <input type="text" name="username">
    <input type="password" name="password">
</form>
```

---

### 9. Anywhere Descendant (double slash)

```java
driver.findElement(By.xpath("//parentTag//descendantTag"));
```
- Example: `//div//input`

**HTML Example:**
```html
<div>
    <section>
        <input type="text" name="search">
    </section>
</div>
```

---

### 10. Select by Index (Nth Element)

```java
driver.findElement(By.xpath("(//tagName[@attribute='value'])[n]"));
```
- Example: `(//input[@type='text'])[2]`

**HTML Example:**
```html
<input type="text" name="first">
<input type="text" name="second">
```

---

### 11. Navigate to Parent

```java
driver.findElement(By.xpath("//childTag/.."));
```
- Example: `//input/..`

**HTML Example:**
```html
<div>
    <input type="text" name="username">
</div>
```

---

### 12. Sibling Navigation (following-sibling)

```java
driver.findElement(By.xpath("//tagName[@attribute='value']/following-sibling::tagName"));
```
- Example: `//label[@for='email']/following-sibling::input`

**HTML Example:**
```html
<label for="email">Email</label>
<input type="email" id="email">
```

---

### 13. Attribute Contains Match (XPath - Regular expression)

```java
driver.findElement(By.xpath("//button[contains(@class,'submit')]"));
```
- Example: `//button[contains(@class,'submit')]`

**HTML Example:**
```html
<button class="btn submit-btn">Submit</button>
```

---

### 14.1 Select Child Element by Index (Div → Button)

```java
driver.findElement(By.xpath("//div[@attribute='value']/childTag[n]"));
```
- Example: `//div[@class='forgot-pwd-btn-conainer']/button[1]`

**HTML Example:**
```html
<div class="forgot-pwd-btn-conainer">
    <button class="go-to-login-btn">Go to Login</button>
    <button class="reset-pwd-btn">Reset Login</button>
</div>
```

---

### 14.2 Select Child Element by Index (Form → Input)

```java
driver.findElement(By.xpath("//parentTag/childTag[n]"));
```
- Example: `//form/input[3]`

**HTML Example:**
```html
<form>
    <input type="text" name="firstName" value="John">
    <input type="text" name="lastName" value="Doe">
    <input type="email" name="email" value="john.doe@example.com">
    <input type="password" name="password">
</form>
```

```java
WebElement thirdInput = driver.findElement(By.xpath("//form/input[3]"));
System.out.println("Third input type: " + thirdInput.getAttribute("type"));  // Output: email
System.out.println("Third input name: " + thirdInput.getAttribute("name"));  // Output: email
```

---

### 15. Select Following Sibling Element

```java
driver.findElement(By.xpath("//header/div/button[1]/following-sibling::button"));
```
- Explanation:
Selects all `<button>` elements that are siblings after the first `<button>` inside a `<div>` under a `<header>`.

**HTML Example:**
```html
<header>
    <div>
        <button id="firstBtn">First</button>
        <button id="secondBtn">Second</button>
        <button id="thirdBtn">Third</button>
    </div>
</header>
```

**Java Example:**
```java
// Get the second button (sibling after the first)
WebElement secondButton = driver.findElement(By.xpath("//header/div/button[1]/following-sibling::button[1]"));
System.out.println("Second button text: " + secondButton.getText());  // Outputs: Second

// Get the third button (second sibling after the first)
WebElement thirdButton = driver.findElement(By.xpath("//header/div/button[1]/following-sibling::button[2]"));
System.out.println("Third button text: " + thirdButton.getText());  // Outputs: Third
```

---

## XPath Structure – Usage

| XPath Structure | When to Use |
|:---|:---|
| `//div[@attribute='value']/button[n]` | When selecting a specific `<button>` inside a `<div>`, such as buttons in modals, popups, or custom containers. |
| `//form/input[n]` | When selecting a specific `<input>` field inside a `<form>`, such as username, email, or password fields in login or signup forms. |
