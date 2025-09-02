# screenshots in selenium webdriver

## overview

Selenium WebDriver provides powerful ways to take screenshots for:

- Full page capture
- Specific element capture
- Base64-encoded screenshots (for embedding in reports)

These are essential for:

- Debugging failed tests
- Visual verification
- Generating test reports

---

## 🖥️ full page screenshot

```java
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.OutputType;
import java.io.File;
import org.apache.commons.io.FileUtils;

File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(src, new File("screenshots/test-failure.png"));
```

### notes

- Stores screenshot in `.png` format.
- Always use unique filenames (e.g. with timestamp).
- Create the folder `screenshots/` beforehand or use `File.mkdirs()`.

---

## specific element screenshot (selenium 4+)

```java
import org.openqa.selenium.WebElement;
import org.openqa.selenium.By;

WebElement logo = driver.findElement(By.id("logo"));
File elementShot = logo.getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(elementShot, new File("screenshots/logo.png"));
```

### notes

- Works only with **Selenium 4+**.
- Captures **only the visible part** of the element.

---

## base64 screenshot (for embedding)

```java
String base64Screenshot = ((TakesScreenshot) driver)
                            .getScreenshotAs(OutputType.BASE64);

// Embed in HTML reports
String imgTag = "<img src='data:image/png;base64," + base64Screenshot + "' />";
```

- Used in HTML-based reports (like ExtentReports, Allure).
- No need to save to disk.

---

## when to capture screenshots

| Scenario        | Use Case                             |
|-----------------|---------------------------------------|
| Test Failure    | Capture the UI state at failure       |
| Visual Testing  | Compare layouts across releases       |
| Test Reporting  | Attach proof of test steps or result  |

---

## 📁 screenshot best practices

1. Use folders like `screenshots/{testName}/` or by date.
2. Name files like `LoginTest_2025-09-02_13-22.png`
3. Clean old screenshots programmatically if needed.
4. Integrate screenshot capture inside failure hooks (`ITestListener`).

---

## 🔁 reusable screenshot utility method

```java
public static void captureScreenshot(WebDriver driver, String fileName) {
    try {
        File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
        String timestamp = new SimpleDateFormat("yyyyMMdd_HHmmss").format(new Date());
        String path = "screenshots/" + fileName + "_" + timestamp + ".png";
        FileUtils.copyFile(src, new File(path));
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

**Usage:**

```java
ScreenshotUtil.captureScreenshot(driver, "LoginTest");
```

---

## integrate with testng listener

```java
@Override
public void onTestFailure(ITestResult result) {
    WebDriver driver = Driver.getDriver(); // Singleton driver instance
    String testName = result.getName();    // Failed test method name
    ScreenshotUtil.captureScreenshot(driver, testName);
}
```

Add `TestListener` to your `testng.xml`:

```xml
<listeners>
    <listener class-name="utils.TestListener" />
</listeners>
```

---

## troubleshooting

| Problem                        | Solution                                      |
|-------------------------------|-----------------------------------------------|
| Screenshot file not saved     | Ensure directory exists or use `.mkdirs()`    |
| `null` WebDriver in Listener  | Use Singleton Driver pattern                  |
| Incomplete screenshot         | Consider using tools like **Ashot** for full-page |
| SLF4J warnings                | Exclude or configure SLF4J dependencies       |
