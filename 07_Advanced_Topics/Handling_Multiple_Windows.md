
# Handling Multiple Windows in Selenium

## What Is a Window in Selenium?

In Selenium, every **browser tab or window** opened by your test is considered a separate window. Selenium assigns each window a **unique window handle** — a string identifier you can use to switch between windows.

Common use cases where multiple windows occur:
- Clicking a link that opens a new tab or window.
- Handling pop-ups or external pages.
- Switching between the main application and an authentication provider (like Google/Facebook login).

---

## Key Selenium Commands

| Command                                      | Purpose                                                 |
|---------------------------------------------|--------------------------------------------------------|
| `driver.getWindowHandle()`                  | Get the handle of the **current** window.               |
| `driver.getWindowHandles()`                 | Get a **set of all window handles** opened by the test. |
| `driver.switchTo().window(handle)`          | Switch to a window using its handle.                   |
| `driver.close()`                            | Close the current window.                              |
| `driver.quit()`                             | Close **all** windows and end the session.             |

---

## General Steps for Handling Multiple Windows

1. **Trigger the action** that opens the new window (e.g., click a link).
2. **Get all window handles** using `getWindowHandles()`.
3. **Identify the child window** (the one that is not the original).
4. **Switch to the child window** using `switchTo().window(childHandle)`.
5. **Perform actions** inside the child window.
6. **Switch back** to the parent window if needed.

---

## Example Code

```java
import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import java.util.Iterator;
import java.util.Set;

public class WindowHandlesExample {
    public static void main(String[] args) {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();

        driver.get("https://rahulshettyacademy.com/loginpagePractise/");

        // Click the link that opens a new window
        driver.findElement(By.cssSelector(".blinkingText")).click();

        // Get window handles
        Set<String> windowHandles = driver.getWindowHandles();
        Iterator<String> iterator = windowHandles.iterator();

        String parentWindow = iterator.next();
        String childWindow = iterator.next();

        // Switch to child window
        driver.switchTo().window(childWindow);
        System.out.println("Child window title: " + driver.getTitle());

        // Perform actions in child window
        String emailText = driver.findElement(By.cssSelector("p.im-para.red")).getText();
        String email = emailText.split("at")[1].trim().split(" ")[0];
        System.out.println("Extracted email: " + email);

        // Switch back to parent window
        driver.switchTo().window(parentWindow);

        driver.quit();
    }
}
```

---

## Tips for Handling Windows

- Always capture the parent window handle **before** opening a new window.  
- After switching to a child window, make sure to close it if not needed to avoid memory leaks.  
- Always switch back to the parent window before continuing interactions.  
- Use `getWindowHandles()` carefully — it returns a **Set**, so ordering is not guaranteed (use iterators or loops carefully).

---

## Best Practices

- **Name Your Windows:** Assign meaningful variables like `parentWindow`, `childWindow` for clarity.
- **Wait for Windows to Open:** Use explicit waits if the child window takes time to appear.
- **Loop Through Windows:** If there are more than two windows, loop through the handles and identify by window title or URL.
- **Clean Up:** Always close child windows when done and return focus to the main window.

---

## Summary

Handling multiple windows is essential for robust Selenium tests when dealing with multi-tab or multi-window applications. By mastering window handles, you ensure your tests can:
- Navigate across external systems.
- Extract and transfer data between windows.
- Maintain stability across complex flows.

*Prepared for automation learners and testers using Selenium WebDriver.*
