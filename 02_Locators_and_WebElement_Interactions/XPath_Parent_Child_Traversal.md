# XPath Parent-Child Traversal

navigate between parent and child elements in XPath for Selenium automation.

---

## 1. Direct Parent-to-Child Traversal

When you want to select a **direct child** element inside a parent.

### Syntax
```java
driver.findElement(By.xpath("//parentTag/childTag"));
```

### Example
```java
driver.findElement(By.xpath("//form/input"));
```

**HTML Example:**
```html
<form>
    <input type="text" name="username">
    <input type="password" name="password">
</form>
```
This XPath selects both `<input>` elements that are direct children of `<form>`.

---

## 2. Descendant Traversal (Anywhere Under Parent)

When you want to select elements **anywhere under** a parent (even nested deeper).

### Syntax
```java
driver.findElement(By.xpath("//parentTag//descendantTag"));
```

### Example
```java
driver.findElement(By.xpath("//div//input"));
```

**HTML Example:**
```html
<div>
    <section>
        <input type="text">
    </section>
</div>
```
This XPath selects the `<input>` element even though it is nested inside `<section>`.

---

## 3. Child-to-Parent Traversal

When you want to go **up** from a child to its parent.

### Syntax
```java
driver.findElement(By.xpath("//childTag/.."));
```

### Example
```java
driver.findElement(By.xpath("//input/.."));
```

**HTML Example:**
```html
<div>
    <input type="text" name="search">
</div>
```
This XPath selects the `<div>` (parent of `<input>`).

---

## 4. Select Specific Child by Index

When you want to select a specific child element by its position.

### Syntax
```java
driver.findElement(By.xpath("//parentTag/childTag[n]"));
```

### Example
```java
driver.findElement(By.xpath("//ul/li[2]"));
```

**HTML Example:**
```html
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```
This XPath selects the second `<li>` element.

---

## Summary Table

| Traversal Type       | Syntax Example                        | Use Case                                   |
|----------------------|--------------------------------------|-------------------------------------------|
| Parent to child      | `//form/input`                       | Direct child element                      |
| Anywhere descendant  | `//div//input`                       | Any level nested element under parent     |
| Child to parent      | `//input/..`                         | Move up to parent element                 |
| Child by index       | `//ul/li[2]`                         | Select nth child element inside a parent  |
