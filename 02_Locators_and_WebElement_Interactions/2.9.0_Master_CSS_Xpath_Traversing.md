**1) Parent — going from the child to its parent**

**xpath**

```
//input[@id='username']/parent::div
```

**css (no direct parent selector, target the parent with `:has()`)**

```css
div:has(> #username)
/* or more specific: .input-wrapper:has(> #username) */
```

**note:** css selectors cannot “go up”; `:has()` selects the parent **conditionally**.

**html**

```html
<div class="input-wrapper">
    <input id="username" type="text">
</div>
```

---

**2) Child — going from the parent to its direct child**

**xpath**

```
//div[@class='form-group']/child::input

```

**css**

```css
.form-group > input
```

**html**

```html
<div class="form-group">
    <input type="text" name="email">
</div>
```

---

**3) Ancestor — any ancestor above**

**xpath**

```
//input[@id='username']/ancestor::form
```

**css (select the ancestor conditionally using `:has()`)**

```css
form:has(#username)
/* more narrow: #loginForm:has(#username) */
```

**html**

```html
<form id="loginForm">
    <div class="input-wrapper">
        <input id="username" type="text">
    </div>
</form>
```

---

**4) Descendant — any descendant below**

**xpath**

```
//form[@id='loginForm']/descendant::input
```

**css**

```css
#loginForm input
/* captures all inputs (including deep nested ones) */
```

**html**

```html
<form id="loginForm">
    <div class="user-info">
        <input type="text" name="firstName">
        <div class="nested">
            <input type="text" name="lastName">
        </div>
    </div>
</form>
```

---

**5) Following-sibling — the next sibling at the same level**

**xpath**

```
//label[@for='username']/following-sibling::input
```

**css (adjacent and general sibling)**

```css
label[for="username"] + input        /* only the immediate next sibling */
label[for="username"] ~ input        /* all following input siblings */
```

**html**

```html
<form>
    <label for="username">username</label>
    <input id="username" type="text">
</form>
```

---

**6) Preceding-sibling — the previous sibling at the same level**

**xpath**

```
//input[@id='username']/preceding-sibling::label
```

**css (cannot go backwards, but can target the “previous label” conditionally)**

```css
label:has(+ #username)   /* selects the label that has #username input right after it */
```

> explanation: css cannot select “previous siblings”; but when selecting the label, you can match it based on the adjacent input condition. this achieves the same target as xpath in practice.
> 

**html**

```html
<form>
    <label for="username">username</label>
    <input id="username" type="text">
</form>
```

---

**Combination example (css equivalent of xpath chain)**

**xpath**

```
//label[text()='Username']/following-sibling::input/ancestor::form
```

**css (label → sibling input → form)**

```css
/* 1) match label by text (pure css cannot do text match) => alternative: use [for="username"] */
label[for="username"] + input        /* finds the input */
form:has(label[for="username"] + input)
/* selects the form if it contains a label + input relationship */
```

> note: css cannot directly match by innertext; so we usually replace text()='username' with something like for="username" or other attributes. if you must match by text, in a test framework (like playwright) you can use pseudo-classes like :has-text() (not native css).
> 

---

**Practical playwright usage (css)**

```tsx
// parent (div.input-wrapper)
const parent = page.locator('div:has(> #username)');

// ancestor form
const form = page.locator('form:has(#username)');

// descendants
const allInputsInForm = page.locator('#loginForm input');

// following sibling
const inputNextToLabel = page.locator('label[for="username"] + input');

// “preceding” sibling effect (css way to find the label)
const labelBeforeInput = page.locator('label:has(+ #username)');
```

**Support / compatibility**

- `:has()` is now supported in modern chromium, firefox, and safari.
- if your ci targets older browsers, plan a fallback strategy (e.g., data-* attributes, extra id/class).
