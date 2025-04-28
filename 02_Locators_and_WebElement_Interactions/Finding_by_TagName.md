# Finding Elements by Tag Name

- Locates elements by HTML tag names like `input`, `button`, `div`, etc.
- Useful for finding multiple elements of the same type.

### Example:
```java
List<WebElement> inputs = driver.findElements(By.tagName("input"));
System.out.println(inputs.size());
