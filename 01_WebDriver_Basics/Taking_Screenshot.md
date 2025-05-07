Screenshots

This document covers **detailed techniques** for capturing screenshots in Selenium WebDriver.

---

## Overview

Selenium's `TakesScreenshot` interface enables you to capture images of:
- The entire page
- Specific elements
- Browser viewport

Screenshots are critical for debugging, reporting, and visual validation.

---

## Capture Full Page Screenshot

```java
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.OutputType;
import java.io.File;
import org.apache.commons.io.FileUtils;

// Take a screenshot of the current page
File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
// Save the screenshot to the specified file path
FileUtils.copyFile(src, new File("/Users/yahyayusifli/Downloads/screenshot.png"));


```

### Notes
- Stores screenshot as a **PNG** or **BASE64** (depending on OutputType).
- Save files with unique names to avoid overwriting.

---

## Capture Element Screenshot

```java
import org.openqa.selenium.WebElement;

WebElement element = driver.findElement(By.id("logo"));
File elementShot = element.getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(elementShot, new File("element.png"));
```

### Notes
- Requires Selenium 4+.
- Captures only the selected element’s visible area.

---

## Capture Base64 Screenshot (for embedding)

```java
String base64Screenshot = ts.getScreenshotAs(OutputType.BASE64);
// You can embed this directly into HTML reports
```

---

## When to Use Screenshots

- **On Failures**: Capture failure states for debugging.
- **Visual Testing**: Compare screenshots across runs.
- **Reports**: Attach screenshots to test result reports.

---

## Best Practices

- Organize screenshots by test case and date.
- Automate cleanup of old screenshots to save space.
- Integrate screenshot capture in your test framework’s failure hooks.

---
