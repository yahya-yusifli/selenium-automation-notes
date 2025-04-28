# Taking Screenshot

Selenium can take screenshots of the browser during test execution.

```java
File screenshot = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
// Save or move the screenshot using FileUtils
