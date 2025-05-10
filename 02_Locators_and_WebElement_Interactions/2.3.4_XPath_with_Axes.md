# XPath with Axes

how to use XPath axes to navigate the document tree relative to a specific node in Selenium automation, with detailed Java examples including outputs and actions.

---

## What Are XPath Axes?

XPath axes define relationships between nodes in the DOM, allowing you to traverse:
- Upward (parent, ancestor)
- Downward (child, descendant)
- Sideways (sibling)
- Across (following, preceding)

These axes help build powerful and flexible locators.

---

## Common XPath Axes with Detailed Java Examples

### 1. child::
Selects all direct child elements.

```java
WebElement inputField = driver.findElement(By.xpath("//div/child::input"));
inputField.sendKeys("test input");
System.out.println("Input field tag: " + inputField.getTagName());
```

**HTML Example:**
```html
<div>
    <input type="text">
    <input type="password">
</div>
```
**Expected Output:**
```
Input field tag: input
```

---

### 2. parent::
Selects the parent node of the current element.

```java
WebElement parentDiv = driver.findElement(By.xpath("//input/parent::div"));
System.out.println("Parent tag: " + parentDiv.getTagName());
```

**HTML Example:**
```html
<div>
    <input type="text">
</div>
```
**Expected Output:**
```
Parent tag: div
```

---

### 3. ancestor::
Selects all ancestor nodes (parents, grandparents, etc.).

```java
WebElement ancestorForm = driver.findElement(By.xpath("//input/ancestor::form"));
System.out.println("Ancestor form found: " + ancestorForm.getAttribute("id"));
```

**HTML Example:**
```html
<form id="loginForm">
    <div>
        <input type="text">
    </div>
</form>
```
**Expected Output:**
```
Ancestor form found: loginForm
```

---

### 4. descendant::
Selects all descendants (children, grandchildren, etc.).

```java
WebElement descendantInput = driver.findElement(By.xpath("//div/descendant::input"));
descendantInput.sendKeys("descendant value");
System.out.println("Descendant input type: " + descendantInput.getAttribute("type"));
```

**HTML Example:**
```html
<div>
    <section>
        <input type="text">
    </section>
</div>
```
**Expected Output:**
```
Descendant input type: text
```

---

### 5. following::
Selects all nodes after the current node in the document.

```java
WebElement followingParagraph = driver.findElement(By.xpath("//h2/following::p"));
System.out.println("Following paragraph text: " + followingParagraph.getText());
```

**HTML Example:**
```html
<h2>Header</h2>
<p>Paragraph 1</p>
<p>Paragraph 2</p>
```
**Expected Output:**
```
Following paragraph text: Paragraph 1
```

---

### 6. preceding::
Selects all nodes before the current node.

```java
WebElement precedingHeader = driver.findElement(By.xpath("//p/preceding::h2"));
System.out.println("Preceding header text: " + precedingHeader.getText());
```

**HTML Example:**
```html
<h2>Header</h2>
<p>Paragraph 1</p>
```
**Expected Output:**
```
Preceding header text: Header
```

---

### 7. following-sibling::
Selects all siblings after the current node.

```java
WebElement followingSiblingPara = driver.findElement(By.xpath("//h2/following-sibling::p"));
System.out.println("Following sibling paragraph: " + followingSiblingPara.getText());
```

**HTML Example:**
```html
<h2>Header</h2>
<p>Paragraph 1</p>
<p>Paragraph 2</p>
```
**Expected Output:**
```
Following sibling paragraph: Paragraph 1
```

---

### 8. preceding-sibling::
Selects all siblings before the current node.

```java
WebElement precedingSiblingHeader = driver.findElement(By.xpath("//p/preceding-sibling::h2"));
System.out.println("Preceding sibling header: " + precedingSiblingHeader.getText());
```

**HTML Example:**
```html
<h2>Header</h2>
<p>Paragraph 1</p>
```
**Expected Output:**
```
Preceding sibling header: Header
```

---

## Summary Table

| Axis                | Purpose                                 | Example Syntax                                   |
|---------------------|----------------------------------------|-------------------------------------------------|
| child::             | Direct children                        | `//div/child::input`                           |
| parent::            | Parent node                            | `//input/parent::div`                          |
| ancestor::          | All ancestor nodes                     | `//input/ancestor::form`                       |
| descendant::        | All descendant nodes                   | `//div/descendant::input`                      |
| following::         | All nodes after current node           | `//h2/following::p`                            |
| preceding::         | All nodes before current node          | `//p/preceding::h2`                            |
| following-sibling:: | Sibling nodes after current node       | `//h2/following-sibling::p`                    |
| preceding-sibling:: | Sibling nodes before current node      | `//p/preceding-sibling::h2`                    |

