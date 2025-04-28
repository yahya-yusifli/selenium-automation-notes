# Finding Single and Multiple Elements

`findElement()` finds a single matching element; `findElements()` finds multiple elements.

```java
WebElement singleElement = driver.findElement(By.id("username"));
List<WebElement> multipleElements = driver.findElements(By.tagName("input"));
