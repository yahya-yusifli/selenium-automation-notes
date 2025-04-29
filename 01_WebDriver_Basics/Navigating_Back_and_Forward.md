# Navigating Back and Forward in Selenium

In Selenium WebDriver, the `navigate()` interface allows you to move through the browser’s history, similar to how a user clicks the back and forward buttons in a browser. This is useful for simulating real-world navigation behavior during test automation.

---

## Key Methods

- **`driver.navigate().to(String url)`**  
  Loads a new web page in the current browser window.

- **`driver.navigate().back()`**  
  Moves one step backward in the browser's history.

- **`driver.navigate().forward()`**  
  Moves one step forward in the browser's history.

---
# Difference Between driver.get() and driver.navigate().to() in Selenium

In Selenium WebDriver, both `driver.get()` and `driver.navigate().to()` are used to open web pages. However, they have slightly different use cases and behaviors.

---

## driver.get()

- Opens a web page and waits until it is fully loaded.
- A simpler and more direct method.
- Commonly used at the beginning of a test.
- Does not maintain browser history for navigation actions.

---

## driver.navigate().to()

- Also opens a web page, but is part of the `navigate()` interface.
- Supports additional navigation methods like `back()`, `forward()`, and `refresh()`.
- Offers more control and flexibility.
- Better suited for simulating real user browsing behavior.

---
- Use **`get()`** when you just need to load a page once.
- Use **`navigate().to()`** when you're testing navigation steps like back and forward between pages.
---
## Example: Full Navigation Flow

This example demonstrates how to use navigation commands in sequence:

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class NavigationExample {
    public static void main(String[] args) {
        // Set the path to your local ChromeDriver executable
        System.setProperty("webdriver.chrome.driver", "/Users/yy/Documents/chromedriver-mac-arm64/chromedriver");

        // Create a Chrome browser instance
        WebDriver driver = new ChromeDriver();

        // Maximize the browser window
        driver.manage().window().maximize();

        // Open Google homepage
        driver.get("http://google.com");

        // Navigate to another site
        driver.navigate().to("https://rahulshettyacademy.com");

        // Go back to Google
        driver.navigate().back();

        // Go forward again to Rahul Shetty Academy
        driver.navigate().forward();

        // Close the browser
        driver.quit();
    }
}
