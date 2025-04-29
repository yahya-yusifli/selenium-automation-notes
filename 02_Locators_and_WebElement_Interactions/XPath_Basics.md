# XPath Basics

- XPath is used to navigate through elements and attributes.
- It supports complex and dynamic element identification.

---
| Locator Type             | XPath Expression                                               | Description                                                                                   | Java Example                                                                                 |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| **Absolute Path**        | `/html/body/div[2]/form/input`                                 | Selects an element by its full path from the document root                                    | `driver.findElement(By.xpath("/html/body/div[2]/form/input"));`                              |
| **Relative Path**        | `//input`                                                      | Selects all `<input>` elements anywhere in the document                                       | `driver.findElement(By.xpath("//input"));`                                                   |
| **Attribute Equals**     | `//tag[@attr='value']`                                         | Selects `<tag>` elements whose `attr` exactly matches `value`                                 | `driver.findElement(By.xpath("//input[@type='email']"));`                                    |
| **Attribute Contains**   | `//tag[contains(@attr,'sub')]`                                 | Selects `<tag>` elements whose `attr` contains the substring `sub`                            | `driver.findElement(By.xpath("//input[contains(@placeholder,'Email')]"));`                   |
| **Starts-With**          | `//tag[starts-with(@attr,'start')]`                            | Selects `<tag>` elements whose `attr` starts with `start`                                     | `driver.findElement(By.xpath("//a[starts-with(@href,'https')]"));`                          |
| **Ends-With**            | `//tag[ends-with(@attr,'end')]`                                | Selects `<tag>` elements whose `attr` ends with `end`                                         | `driver.findElement(By.xpath("//img[ends-with(@src,'.png')]"));`                             |
| **Text Equals**          | `//tag[text()='value']`                                        | Selects `<tag>` elements whose exact text content is `value`                                  | `driver.findElement(By.xpath("//button[text()='Submit']"));`                                 |
| **Text Contains**        | `//tag[contains(text(),'part')]`                              | Selects `<tag>` elements whose text contains `part`                                           | `driver.findElement(By.xpath("//p[contains(text(),'successfully')]"));`                      |
| **Multiple Attributes**  | `//tag[@a='1' and @b='2']`                                     | Selects `<tag>` elements that satisfy **both** attribute conditions                           | `driver.findElement(By.xpath("//input[@type='text' and @name='username']"));`                |
| **OR Condition**         | `//tag[@a='1' or @b='2']`                                      | Selects `<tag>` elements that satisfy **either** attribute condition                          | `driver.findElement(By.xpath("//input[@id='user' or @name='login']"));`                      |
| **Indexing**             | `(//tag)[n]`                                                   | Selects the **nᵗʰ** `<tag>` element in document order (1-based)                                | `driver.findElement(By.xpath("(//input)[3]"));`                                              |
| **Last Element**         | `(//tag)[last()]`                                              | Selects the **last** `<tag>` element in document order                                        | `driver.findElement(By.xpath("(//li)[last()]"));`                                            |
| **Position**             | `//tag[position()=n]`                                          | Selects `<tag>` elements whose position among siblings is **n**                               | `driver.findElement(By.xpath("//ul/li[position()=2]"));`                                      |
| **Wildcard**             | `//*`                                                          | Selects **any** element in the document                                                        | `driver.findElement(By.xpath("//*"));`                                                       |
| **Descendant**           | `//div//span`                                                  | Selects all `<span>` elements at **any depth** under `<div>`                                   | `driver.findElement(By.xpath("//div//span"));`                                               |
| **Child**                | `//ul/li`                                                      | Selects `<li>` elements that are **direct** children of `<ul>`                                 | `driver.findElement(By.xpath("//ul/li"));`                                                   |
| **Parent**               | `//input/..`                                                   | Selects the **parent** of every `<input>` element                                              | `driver.findElement(By.xpath("//input[@id='q']/.."));`                                       |
| **Ancestor**             | `//span/ancestor::div`                                         | Selects all `<div>` ancestors of each `<span>`                                                | `driver.findElement(By.xpath("//span[@class='icon']/ancestor::div"));`                       |
| **Following-Sibling**    | `//label/following-sibling::input`                             | Selects `<input>` siblings **immediately** after `<label>`                                     | `driver.findElement(By.xpath("//label[text()='Email']/following-sibling::input"));`          |
| **General-Sibling**      | `//h2/preceding-sibling::p`                                    | Selects **all** `<p>` siblings **before** each `<h2>`                                          | `driver.findElement(By.xpath("//h2[@id='title']/preceding-sibling::p"));`                     |
| **Normalize-Space Text** | `//p[normalize-space(text())='trimmed text']`                 | Selects `<p>` whose text, after trimming whitespace, equals `trimmed text`                     | `driver.findElement(By.xpath("//p[normalize-space(text())='Hello World']"));`                 |

---
### 1. Select by Tag Name

```java
driver.findElement(By.xpath("//tagName"));
```
- Example: `//input`

---

### 2. Select by Attribute

```java
driver.findElement(By.xpath("//tagName[@attribute='value']"));
```
- Example: `//input[@id='username']`

---

### 3. Select by Multiple Attributes

```java
driver.findElement(By.xpath("//tagName[@attribute1='value' and @attribute2='value']"));
```
- Example: `//input[@type='text' and @placeholder='Email']`

---

### 4. Select by Text Content

```java
driver.findElement(By.xpath("//tagName[text()='Exact Text']"));
```
- Example: `//button[text()='Login']`

---

### 5. Select by Partial Text (contains)

```java
driver.findElement(By.xpath("//tagName[contains(text(),'PartialText')]"));
```
- Example: `//button[contains(text(),'Log')]`

---

### 6. Select by Attribute Contains

```java
driver.findElement(By.xpath("//tagName[contains(@attribute,'partialValue')]"));
```
- Example: `//input[contains(@placeholder,'mail')]`

---

### 7. Select by Attribute Starts-With

```java
driver.findElement(By.xpath("//tagName[starts-with(@attribute,'valueStart')]"));
```
- Example: `//input[starts-with(@id,'user')]`

---

### 8. Parent to Child Selection

```java
driver.findElement(By.xpath("//parentTag/childTag"));
```
- Example: `//form/input`

---

### 9. Anywhere Descendant (double slash)

```java
driver.findElement(By.xpath("//parentTag//descendantTag"));
```
- Example: `//div//input`

---

### 10. Select by Index (Nth Element)

```java
driver.findElement(By.xpath("(//tagName[@attribute='value'])[n]"));
```
- Example: `(//input[@type='text'])[2]`

---

### 11. Navigate to Parent

```java
driver.findElement(By.xpath("//childTag/.."));
```
- Example: `//input/..` (goes to input's parent)

---

### 12. Sibling Navigation (following-sibling)

```java
driver.findElement(By.xpath("//tagName[@attribute='value']/following-sibling::tagName"));
```
- Example: `//label[@for='email']/following-sibling::input`

---
### 13. Attribute Contains Match (XPath - Regular expression)

```java
driver.findElement(By.xpath("//button[contains(@class,'submit')]"));
```
- Example: `//button[contains(@class,'submit')]`

---
### 14.1 Select Child Element by Index (Div → Button)

```java
driver.findElement(By.xpath("//div[@attribute='value']/childTag[n]"));
```
Example: `//div[@class='forgot-pwd-btn-conainer']/button[1]`
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
Example: `//form/input[3]`

 ## XPath Structure – Usage

| XPath Structure | When to Use |
|:---|:---|
| `//div[@attribute='value']/button[n]` | When selecting a specific `<button>` inside a `<div>`, such as buttons in modals, popups, or custom containers. |
| `//form/input[n]` | When selecting a specific `<input>` field inside a `<form>`, such as username, email, or password fields in login or signup forms. |

---

