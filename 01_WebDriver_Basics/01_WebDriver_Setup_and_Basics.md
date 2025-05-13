**01 – WebDriver Setup and Basics**

---
**1. Setting Up WebDriver**

**Import Required Packages**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
```

**WebDriver Setup Example**
```java
System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
WebDriver driver = new ChromeDriver();
```

Or with WebDriverManager:
```java
WebDriverManager.chromedriver().setup();
WebDriver driver = new ChromeDriver();
```

---

**2. WebDriver Interface and Browser Drivers**

- `WebDriver` is an interface implemented by browser-specific classes like `ChromeDriver`, `FirefoxDriver`, etc.
- Each browser requires its own driver:
  - Chrome → chromedriver
  - Firefox → geckodriver
  - Edge → msedgedriver

**Common Implementations:**
```java
WebDriver driver = new ChromeDriver();
WebDriver driver = new FirefoxDriver();
WebDriver driver = new EdgeDriver();
```

---

**3. Launching a Browser**

**Open Chrome Browser and Maximize**
```java
WebDriver driver = new ChromeDriver();
driver.manage().window().maximize();
```

---

**4. Opening a URL with `.get()`**
```java
driver.get("https://example.com");
```
This method opens the specified URL and waits for the page to load completely.

---

**5. Common Browser Commands**

**Get Page Title**
```java
String title = driver.getTitle();
System.out.println("Page Title: " + title);
```

**Get Current URL**
```java
String url = driver.getCurrentUrl();
System.out.println("Current URL: " + url);
```

**Navigate to Another Page**
```java
driver.navigate().to("https://another-page.com");
```

**Go Back and Forward**
```java
driver.navigate().back();
driver.navigate().forward();
```

**Refresh the Page**
```java
driver.navigate().refresh();
```

---

**6. Closing and Quitting the Browser**

**Close the Current Window**
```java
driver.close();
```

**Quit All Browser Windows**
```java
driver.quit();
```

---

**Summary Table**

| Action                | Method                        |
|-----------------------|-------------------------------|
| Open URL              | `driver.get(url)`             |
| Maximize Window       | `driver.manage().window().maximize()` |
| Get Title             | `driver.getTitle()`           |
| Get Current URL       | `driver.getCurrentUrl()`      |
| Navigate To           | `driver.navigate().to(url)`   |
| Back / Forward        | `driver.navigate().back()` / `forward()` |
| Refresh Page          | `driver.navigate().refresh()` |
| Close Window          | `driver.close()`              |
| Quit Browser          | `driver.quit()`               |

