# XPath Basics

- XPath is used to navigate through elements and attributes.
- It supports complex and dynamic element identification.

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
### 13. Attribute Contains Match (XPath)

```java
driver.findElement(By.xpath("//button[contains(@class,'submit')]"));
```
- Example: `//button[contains(@class,'submit')]`
