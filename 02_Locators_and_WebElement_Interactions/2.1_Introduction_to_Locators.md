# Introduction to Locators

Locators are the key to interacting with web elements in Selenium automation.  
They help Selenium find buttons, text fields, links, and other components on a web page.  
Choosing the right locator improves the stability, reliability, and speed of test scripts.

Types of Locators:
- ID
- Name
- Class Name
- Tag Name
- Link Text / Partial Link Text
- CSS Selector
- XPath

# Locator Strategies and Cheat Sheets

## Introduction to Locators

- **Locators** are used to **identify HTML elements** on a webpage so Selenium can interact with them.
- Selenium WebDriver provides multiple locator strategies:

| **Locator Type** | **Example** |
| --- | --- |
| id | id="inputUsername" |
| xpath | //input[@id='inputUsername'] |
| css selector | input#inputUsername |
| name | name="username" |
| className | class="input-field" |
| tagName | input, button, div |
| linkText | Match the entire link text |
| partialLinkText | Match part of the link text |

Example HTML:

```html
<input type="text" placeholder="Username" id="inputUsername" value="">
```

| **Component** | **What It Is** |
| --- | --- |
| input | Tag name |
| type, placeholder, id, value | Attributes |
| "Username", "inputUsername", "" | Attribute values |

---

# CSS Selector Notes

Website to practice: [Rahul Shetty Academy Locator Practice](https://rahulshettyacademy.com/locatorspractice/)

---

# CSS Selector Strategies Explained (with Example)

Example HTML:

```html
<p class="error">* Incorrect username or password </p>
```

## 1. By Class Name

- **Syntax:** .classname
- **CSS Selector:** `.error`
- **Explanation:** Selects an element with the class `error`.

---

## 2. By Tag Name + Class Name

- **Syntax:** tagname.classname
- **CSS Selector:** `p.error`
- **Explanation:** Selects a `<p>` tag with class `error`.

---

## 3. By Attribute

- **Syntax:** tagname[attribute='value']
- **CSS Selector:** `p[class='error']`
- **Explanation:** Selects a `<p>` tag where class equals "error".

---

## 4. By Partial Match with Attribute (contains)

- **Syntax:** tagname[attribute*='partialValue']
- **CSS Selector:** `p[class*='err']`
- **Explanation:** Selects a `<p>` tag where class attribute **contains** "err".

---

## 5. Parent to Child

Example HTML:

```html
<div class="container">
    <p class="error">* Incorrect username or password </p>
</div>
```

- **Syntax:** parenttagname childtagname
- **CSS Selector:** `div p`
- **Explanation:** Selects a `<p>` inside a `<div>`.

---

## Clarification: What is Tag Name?

- Tag names are the HTML element types.
  - Examples: `<input>`, `<button>`, `<div>`, `<h1>`, `<a>`, etc.
- You use the tag name when building locators.

Example:

```html
<button class="signInBtn">Sign In</button>
```

- Tag: `button`
- Class: `signInBtn`
- CSS Selector: `button.signInBtn`

---

# Selenium WebDriver Locators Quick Sheet

| **Locator Type** | **Syntax Example** | **Meaning** |
| --- | --- | --- |
| ID | driver.findElement(By.id("inputUsername")); | Find element by id attribute |
| Name | driver.findElement(By.name("username")); | Find element by name attribute |
| Class Name | driver.findElement(By.className("input-field")); | Find element by class attribute |
| Tag Name | driver.findElement(By.tagName("input")); | Find element by tag name |
| Link Text | driver.findElement(By.linkText("Forgot password?")); | Find link by full text |
| Partial Link Text | driver.findElement(By.partialLinkText("Forgot")); | Find link by partial text |
| XPath | driver.findElement(By.xpath("//input[@id='inputUsername']")); | Find using XPath |
| CSS Selector | driver.findElement(By.cssSelector("input#inputUsername")); | Find using CSS selector |

---

# CSS Selector Cheat Sheet

| **CSS Strategy** | **Syntax Example** | **Notes** |
| --- | --- | --- |
| By Class | .classname | .error, .signInBtn |
| By ID | #id | #inputUsername |
| Tag + Class | tagname.classname | button.signInBtn |
| Tag + ID | tagname#id | input#inputUsername |
| Attribute Equals | tagname[attribute='value'] | input[placeholder='Username'] |
| Attribute Contains | tagname[attribute*='value'] | input[type*='pass'] |
| Parent to Child | parent child | form input |
| First Child / nth Child | parent:nth-child(n) | div:nth-child(2) |

---

# XPath Cheat Sheet

| **XPath Strategy** | **Syntax Example** | **Notes** |
| --- | --- | --- |
| Absolute Path (not recommended) | /html/body/div/input | Full hardcoded path |
| Relative Path | //input[@id='inputUsername'] | Starts anywhere in DOM |
| Using Text | //button[text()='Sign In'] | Match element by visible text |
| Contains Text | //button[contains(text(),'Sign')] | Match partial text |
| Contains Attribute Value | //input[contains(@type,'pass')] | Match attribute that contains |
| Starts-with Attribute | //input[starts-with(@id,'user')] | Match attribute that starts with |
| Parent to Child (direct) | //div/input | Child input inside div |
| Find nth Element | (//input[@type='text'])[2] | Find second matching element |

---

# Example HTML Element and All Possible Locators

```html
<input type="text" placeholder="Username" id="inputUsername" class="input-field" name="username">
```

**Possible locators:**
- By ID: `input#inputUsername` (CSS) or `//input[@id='inputUsername']` (XPath)
- By Name: `By.name("username")`
- By Class: `input.input-field`
- By Tag Name: `By.tagName("input")`
- By Attribute (CSS): `input[placeholder='Username']`
- By Partial Attribute (CSS): `input[placeholder*='User']`

---

# Summary Shortcuts

| **If You Have…** | **Use** |
| --- | --- |
| ID | Prefer id |
| Unique Name | Use name |
| No ID or Name, but has Class | Use className or CSS selector |
| Complex structure | Use XPath |
| Visible link text | Use linkText or partialLinkText |
