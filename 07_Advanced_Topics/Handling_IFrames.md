# Selenium Frames and Nested Frames

## What is a Frame?

A **frame** (or **iframe**) is an HTML element that allows embedding another HTML document inside the main web page.  
This creates a nested structure where you have multiple document contexts on the same page.

From Selenium's perspective:
- You **cannot directly access** elements inside a frame or iframe.
- You **must switch** into the correct frame context before interacting with its elements.

---

## Why Are Frames Important in Automation?

Many real-world applications use iframes to embed components such as:
- Payment forms
- Maps
- Embedded videos (e.g., YouTube)
- Ads or widgets

Without properly handling frames, your Selenium scripts will fail to locate elements inside these embedded sections.

---

## How to Work with Frames in Selenium

| Selenium Command                            | Purpose                                                    |
|--------------------------------------------|-----------------------------------------------------------|
| `driver.switchTo().frame(String nameOrId)`  | Switch to a frame by its name or ID attribute.             |
| `driver.switchTo().frame(int index)`        | Switch to a frame by its index (0-based order on the page).|
| `driver.switchTo().frame(WebElement frame)` | Switch to a frame using a located WebElement reference.    |
| `driver.switchTo().parentFrame()`           | Move back one level to the parent frame.                  |
| `driver.switchTo().defaultContent()`        | Return to the top-level (main page) context.              |

---

## General Steps for Frame Handling

1. Identify the frame you need to work in (check its `name`, `id`, or `index`).
2. Use `switchTo().frame(...)` to enter the frame.
3. Perform the necessary actions inside the frame (locate elements, click, send keys, etc.).
4. Use `switchTo().parentFrame()` or `switchTo().defaultContent()` to return back.

---

## Code Example

```java
// Setup WebDriver
WebDriver driver = new ChromeDriver();
driver.get("https://example.com/page-with-iframe");

// Switch into the iframe by name or ID
driver.switchTo().frame("iframeName");

// Now interact with elements inside the iframe
WebElement insideElement = driver.findElement(By.id("elementInsideIframe"));
insideElement.click();

// Return to the main page
driver.switchTo().defaultContent();
```
---


## Example: Accessing the Middle Frame (Heroku Nested Frames)

Test page:  
https://the-internet.herokuapp.com/nested_frames

Page layout:
```
+-------------------------------------+
|             frame-top               |
| +--------+-----------+----------+   |
| | left   |  middle   | right    |  |
| +--------+-----------+----------+  |
|             frame-bottom           |
+-------------------------------------+
```

Goal: Access the **middle** frame text.

```java
import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class NestedFramesExample {
    public static void main(String[] args) {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();

        driver.get("https://the-internet.herokuapp.com/nested_frames");

        // Step 1: Switch to the outer frame (frame-top)
        driver.switchTo().frame("frame-top");

        // Step 2: Switch to the nested frame (frame-middle)
        driver.switchTo().frame("frame-middle");

        // Step 3: Find the element inside middle frame
        WebElement middle = driver.findElement(By.id("content"));
        System.out.println("Middle frame text: " + middle.getText());  // Outputs: MIDDLE

        // Optional: Go back to the main page context
        driver.switchTo().defaultContent();

        driver.quit();
    }
}
```

Notes:
- Use `frame-top` to enter the top section.
- Use `frame-middle` to enter the middle area inside the top.
- Use `driver.switchTo().defaultContent()` to return to the main page.
