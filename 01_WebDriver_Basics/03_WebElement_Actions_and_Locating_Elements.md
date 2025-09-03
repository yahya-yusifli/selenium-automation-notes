**03 – Locating Elements and WebElement Actions**

locate and interact with elements on a web page using Selenium WebDriver. It also introduces the `Actions` class for advanced user interactions.

---

**1. Finding a Single Element**
```java
WebElement element = driver.findElement(By.id("username"));
element.sendKeys("admin");
```

**Common Locator Strategies:**
- `By.id("id")`
- `By.name("name")`
- `By.className("class")`
- `By.cssSelector("tag[attribute='value']")`
- `By.xpath("//tag[@attribute='value']")`

---

**2. Finding Multiple Elements**
```java
List<WebElement> links = driver.findElements(By.tagName("a"));
System.out.println("Number of links: " + links.size());
```

---

**3. Basic WebElement Actions**

**Click**
```java
driver.findElement(By.id("submitBtn")).click();
```
Click on a button, checkbox, link, or any clickable element.

**Send Keys (Typing into Input Field)**
```java
driver.findElement(By.name("username")).sendKeys("myUsername");
```
Used for entering text into input boxes.

**Clear Input Field**
```java
driver.findElement(By.id("email")).clear();
```
Clears any existing text from a text box.

**Get Text from Element**
```java
String message = driver.findElement(By.id("message")).getText();
System.out.println("Message: " + message);
```

**Get Attribute Value**
```java
String placeholder = driver.findElement(By.id("email")).getAttribute("placeholder");
```

**Is Displayed / Is Enabled / Is Selected**
```java
boolean visible = driver.findElement(By.id("logo")).isDisplayed();
boolean enabled = driver.findElement(By.id("submitBtn")).isEnabled();
boolean selected = driver.findElement(By.id("termsCheckbox")).isSelected();
```

**Submit Form**
```java
driver.findElement(By.id("loginForm")).submit();
```

---

**4. Advanced Actions Using `Actions` Class**
The `Actions` class is used to simulate complex user interactions like hover, right-click, double-click, drag and drop.

**Hover Over Element**
```java
Actions actions = new Actions(driver);
WebElement menu = driver.findElement(By.id("menu"));
actions.moveToElement(menu).perform();
```

**Right Click (Context Click)**
```java
WebElement element = driver.findElement(By.id("target"));
actions.contextClick(element).perform();
```

**Double Click**
```java
WebElement button = driver.findElement(By.id("doubleClick"));
actions.doubleClick(button).perform();
```

**Drag and Drop**
```java
WebElement source = driver.findElement(By.id("source"));
WebElement target = driver.findElement(By.id("target"));
actions.dragAndDrop(source, target).perform();
```

**Send Keys with Keyboard Modifier**
```java
actions.keyDown(Keys.SHIFT).sendKeys("selenium").keyUp(Keys.SHIFT).perform();
```

---

**Example: Using Multiple Actions Together**
```java
WebElement emailInput = driver.findElement(By.id("email"));
emailInput.clear();
emailInput.sendKeys("example@domain.com");

WebElement loginBtn = driver.findElement(By.id("submit"));
if (loginBtn.isEnabled()) {
    loginBtn.click();
}
```

---

**Summary Table**

| Action Type         | Method/Usage                                 |
|---------------------|-----------------------------------------------|
| Click               | `click()`                                     |
| Type Text           | `sendKeys("text")`                            |
| Clear Text          | `clear()`                                     |
| Get Text            | `getText()`                                   |
| Get Attribute       | `getAttribute("name")`                        |
| Is Displayed        | `isDisplayed()`                               |
| Is Enabled          | `isEnabled()`                                 |
| Is Selected         | `isSelected()`                                |
| Submit Form         | `submit()`                                    |
| Hover               | `moveToElement(element).perform()`            |
| Right Click         | `contextClick(element).perform()`             |
| Double Click        | `doubleClick(element).perform()`              |
| Drag and Drop       | `dragAndDrop(source, target).perform()`       |
| Key Combinations    | `keyDown(Keys.SHIFT)...keyUp().perform()`     |

