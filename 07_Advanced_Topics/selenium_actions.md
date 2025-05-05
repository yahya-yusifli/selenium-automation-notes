# Selenium Advanced User Interactions

The Selenium WebDriver's Advanced User Interactions API allows us to perform operations from keyboard events and simple mouse events to complex gestures such as drag-and-drop, click-and-hold, and composite sequences—just like a real user.

The `Actions` class implements the **Builder Pattern**, letting you chain low-level actions into a single composite event.

---

## Creating an Actions Instance

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.interactions.Actions;

// Instantiate the Actions builder
Actions builder = new Actions(driver);
```

- **`driver`**: your active `WebDriver` instance.
- **`builder`**: used to chain interaction methods.

---

## Common Builder Methods

| Method                                      | Description                                                      |
|---------------------------------------------|------------------------------------------------------------------|
| `click(WebElement element)`                 | Clicks (press and release) on the given element.                 |
| `doubleClick(WebElement element)`           | Performs a double click on the element.                          |
| `contextClick(WebElement element)`          | Performs a right-click (context click) on the element.           |
| `clickAndHold(WebElement element)`          | Clicks without releasing at the element’s location.              |
| `release(WebElement element)`               | Releases the mouse at the current location (after `clickAndHold`).|
| `moveToElement(WebElement element)`         | Moves the mouse to the center of the element.                    |
| `sendKeys(CharSequence... keys)`            | Sends a series of keystrokes to the current focus.               |
| `keyDown(Keys key)`                         | Simulates pressing (but not releasing) a modifier key.           |
| `keyUp(Keys key)`                           | Simulates releasing a modifier key.                              |
| `dragAndDrop(WebElement src, WebElement tgt)` | Click-and-hold on `src`, move to `tgt`, then release.           |

---

## Building & Performing the Action

```java
// Example: Drag-and-drop element A onto element B
WebElement source = driver.findElement(By.id("draggable"));
WebElement target = driver.findElement(By.id("droppable"));

builder
    .clickAndHold(source)
    .moveToElement(target)
    .release()
    .build()
    .perform();
```

- **`build()`**: Constructs the composite `Action`.  
- **`perform()`**: Sends the action sequence to the browser.

---

## Tips & Best Practices

- Always import **`org.openqa.selenium.interactions.Actions`** (not AWT).  
- Chain methods in a logical order before calling `build()` and `perform()`.  
- For simple single actions (like a single click), you can skip `build()` and call `perform()` directly on the builder.  

---
