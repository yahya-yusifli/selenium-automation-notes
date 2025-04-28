# Basic WebElement Actions

Perform basic actions like typing text, clicking buttons, clearing fields.

```java
driver.findElement(By.id("inputUsername")).sendKeys("testuser");
driver.findElement(By.className("signInBtn")).click();
