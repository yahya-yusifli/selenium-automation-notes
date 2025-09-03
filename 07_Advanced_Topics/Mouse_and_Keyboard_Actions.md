# Mouse and Keyboard Actions in Selenium

## Overview

Mouse and Keyboard Actions in Selenium allow you to perform **complex user interactions** that go beyond simple `click()` and `sendKeys()` methods. These actions help simulate real user behavior for comprehensive testing.

## Why Use Mouse and Keyboard Actions?

**Basic Selenium limitations:**
```java
// These won't work for complex interactions:
element.click(); // Can't do right-click, double-click, drag
element.sendKeys("text"); // Can't do keyboard shortcuts, key combinations
```

**Advanced Actions solve:**
- **Right-click context menus**
- **Drag and drop operations**
- **Hover effects and tooltips**
- **Keyboard shortcuts (Ctrl+C, Ctrl+V)**
- **Key combinations**
- **Mouse movements**

## Actions Class - The Foundation

The **Actions class** is the main tool for performing advanced mouse and keyboard operations.

```java
import org.openqa.selenium.interactions.Actions;

// Initialize Actions
WebDriver driver = new ChromeDriver();
Actions actions = new Actions(driver);
```

## Mouse Actions

### 1. Basic Mouse Operations

```java
public class BasicMouseActions {
    private WebDriver driver;
    private Actions actions;
    
    public BasicMouseActions(WebDriver driver) {
        this.driver = driver;
        this.actions = new Actions(driver);
    }
    
    // Right click on element
    public void rightClick(WebElement element) {
        actions.contextClick(element).perform();
    }
    
    // Double click on element
    public void doubleClick(WebElement element) {
        actions.doubleClick(element).perform();
    }
    
    // Hover over element
    public void hoverOver(WebElement element) {
        actions.moveToElement(element).perform();
    }
    
    // Click and hold
    public void clickAndHold(WebElement element) {
        actions.clickAndHold(element).perform();
    }
    
    // Release mouse button
    public void release() {
        actions.release().perform();
    }
}
```

### 2. Drag and Drop Operations

```java
public class DragDropActions {
    private Actions actions;
    
    public DragDropActions(WebDriver driver) {
        this.actions = new Actions(driver);
    }
    
    // Drag element from source to target
    public void dragAndDrop(WebElement source, WebElement target) {
        actions.dragAndDrop(source, target).perform();
    }
    
    // Drag element by offset (x, y pixels)
    public void dragAndDropByOffset(WebElement element, int xOffset, int yOffset) {
        actions.dragAndDropBy(element, xOffset, yOffset).perform();
    }
    
    // Manual drag and drop (more control)
    public void manualDragAndDrop(WebElement source, WebElement target) {
        actions.clickAndHold(source)
               .moveToElement(target)
               .release()
               .perform();
    }
    
    // Drag with pause (for slow animations)
    public void dragWithPause(WebElement source, WebElement target, int pauseMs) {
        actions.clickAndHold(source)
               .pause(pauseMs)
               .moveToElement(target)
               .pause(pauseMs)
               .release()
               .perform();
    }
}
```

### 3. Mouse Movement and Positioning

```java
public class MouseMovementActions {
    private Actions actions;
    
    public MouseMovementActions(WebDriver driver) {
        this.actions = new Actions(driver);
    }
    
    // Move to element center
    public void moveToElement(WebElement element) {
        actions.moveToElement(element).perform();
    }
    
    // Move to element with offset
    public void moveToElementWithOffset(WebElement element, int xOffset, int yOffset) {
        actions.moveToElement(element, xOffset, yOffset).perform();
    }
    
    // Move by offset from current position
    public void moveByOffset(int xOffset, int yOffset) {
        actions.moveByOffset(xOffset, yOffset).perform();
    }
    
    // Move to coordinates (from top-left corner)
    public void moveToCoordinates(int x, int y) {
        actions.moveByOffset(x, y).perform();
    }
}
```

## Keyboard Actions

### 1. Basic Keyboard Operations

```java
public class BasicKeyboardActions {
    private Actions actions;
    
    public BasicKeyboardActions(WebDriver driver) {
        this.actions = new Actions(driver);
    }
    
    // Send single key
    public void sendKey(Keys key) {
        actions.sendKeys(key).perform();
    }
    
    // Send key to specific element
    public void sendKeyToElement(WebElement element, Keys key) {
        actions.sendKeys(element, key).perform();
    }
    
    // Press and hold key
    public void keyDown(Keys key) {
        actions.keyDown(key).perform();
    }
    
    // Release key
    public void keyUp(Keys key) {
        actions.keyUp(key).perform();
    }
    
    // Type text
    public void typeText(String text) {
        actions.sendKeys(text).perform();
    }
}
```

### 2. Key Combinations and Shortcuts

```java
public class KeyboardShortcuts {
    private Actions actions;
    
    public KeyboardShortcuts(WebDriver driver) {
        this.actions = new Actions(driver);
    }
    
    // Copy (Ctrl+C)
    public void copy() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys("c")
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Paste (Ctrl+V)
    public void paste() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys("v")
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Select All (Ctrl+A)
    public void selectAll() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys("a")
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Undo (Ctrl+Z)
    public void undo() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys("z")
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Save (Ctrl+S)
    public void save() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys("s")
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Find (Ctrl+F)
    public void find() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys("f")
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Tab navigation
    public void tabForward() {
        actions.sendKeys(Keys.TAB).perform();
    }
    
    public void tabBackward() {
        actions.keyDown(Keys.SHIFT)
               .sendKeys(Keys.TAB)
               .keyUp(Keys.SHIFT)
               .perform();
    }
    
    // Arrow key navigation
    public void arrowUp() {
        actions.sendKeys(Keys.ARROW_UP).perform();
    }
    
    public void arrowDown() {
        actions.sendKeys(Keys.ARROW_DOWN).perform();
    }
    
    public void arrowLeft() {
        actions.sendKeys(Keys.ARROW_LEFT).perform();
    }
    
    public void arrowRight() {
        actions.sendKeys(Keys.ARROW_RIGHT).perform();
    }
}
```

### 3. Complex Key Sequences

```java
public class ComplexKeySequences {
    private Actions actions;
    
    public ComplexKeySequences(WebDriver driver) {
        this.actions = new Actions(driver);
    }
    
    // Multiple key combination (Ctrl+Shift+N)
    public void ctrlShiftN() {
        actions.keyDown(Keys.CONTROL)
               .keyDown(Keys.SHIFT)
               .sendKeys("n")
               .keyUp(Keys.SHIFT)
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Alt+Tab (Switch windows)
    public void altTab() {
        actions.keyDown(Keys.ALT)
               .sendKeys(Keys.TAB)
               .keyUp(Keys.ALT)
               .perform();
    }
    
    // Function key with modifier (Ctrl+F5)
    public void ctrlF5() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys(Keys.F5)
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Chain multiple actions
    public void complexSequence() {
        actions.keyDown(Keys.CONTROL)
               .sendKeys("a")      // Select all
               .keyUp(Keys.CONTROL)
               .sendKeys(Keys.DELETE) // Delete selected
               .sendKeys("New text")  // Type new text
               .perform();
    }
}
```

## Combined Mouse and Keyboard Actions

### 1. Mouse + Keyboard Combinations

```java
public class CombinedActions {
    private Actions actions;
    
    public CombinedActions(WebDriver driver) {
        this.actions = new Actions(driver);
    }
    
    // Click while holding Ctrl (for multi-select)
    public void ctrlClick(WebElement element) {
        actions.keyDown(Keys.CONTROL)
               .click(element)
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Click while holding Shift (for range select)
    public void shiftClick(WebElement element) {
        actions.keyDown(Keys.SHIFT)
               .click(element)
               .keyUp(Keys.SHIFT)
               .perform();
    }
    
    // Right-click and select menu option
    public void rightClickAndSelect(WebElement element, String menuText) {
        // Right-click to open context menu
        actions.contextClick(element).perform();
        
        // Find and click menu option
        WebElement menuOption = driver.findElement(By.xpath("//span[text()='" + menuText + "']"));
        menuOption.click();
    }
    
    // Drag with keyboard modifier
    public void dragWithCtrl(WebElement source, WebElement target) {
        actions.keyDown(Keys.CONTROL)
               .dragAndDrop(source, target)
               .keyUp(Keys.CONTROL)
               .perform();
    }
    
    // Hover and press key
    public void hoverAndPressKey(WebElement element, Keys key) {
        actions.moveToElement(element)
               .sendKeys(key)
               .perform();
    }
}
```

## Practical Examples

### 1. Form Interactions

```java
public class FormActions {
    private WebDriver driver;
    private Actions actions;
    
    public FormActions(WebDriver driver) {
        this.driver = driver;
        this.actions = new Actions(driver);
    }
    
    @Test
    public void testFormNavigation() {
        driver.get("https://example.com/form");
        
        // Tab through form fields
        WebElement firstField = driver.findElement(By.id("firstName"));
        firstField.click();
        
        // Fill first field and tab to next
        actions.sendKeys("John")
               .sendKeys(Keys.TAB)
               .sendKeys("Doe")
               .sendKeys(Keys.TAB)
               .sendKeys("john.doe@example.com")
               .perform();
        
        // Submit using Enter key
        actions.sendKeys(Keys.ENTER).perform();
    }
    
    @Test
    public void testTextSelection() {
        driver.get("https://example.com/editor");
        
        WebElement textArea = driver.findElement(By.id("editor"));
        textArea.sendKeys("This is sample text for testing");
        
        // Select all text
        actions.keyDown(Keys.CONTROL)
               .sendKeys("a")
               .keyUp(Keys.CONTROL)
               .perform();
        
        // Copy selected text
        actions.keyDown(Keys.CONTROL)
               .sendKeys("c")
               .keyUp(Keys.CONTROL)
               .perform();
        
        // Clear field and paste
        textArea.clear();
        actions.keyDown(Keys.CONTROL)
               .sendKeys("v")
               .keyUp(Keys.CONTROL)
               .perform();
    }
}
```

### 2. Drag and Drop Examples

```java
public class DragDropExamples {
    private WebDriver driver;
    private Actions actions;
    
    @Test
    public void testDragDropList() {
        driver.get("https://example.com/sortable-list");
        
        WebElement item1 = driver.findElement(By.id("item1"));
        WebElement item3 = driver.findElement(By.id("item3"));
        
        // Drag item1 to position of item3
        actions.dragAndDrop(item1, item3).perform();
        
        // Verify new order
        List<WebElement> items = driver.findElements(By.cssSelector(".list-item"));
        Assert.assertEquals("item2", items.get(0).getAttribute("id"));
        Assert.assertEquals("item3", items.get(1).getAttribute("id"));
        Assert.assertEquals("item1", items.get(2).getAttribute("id"));
    }
    
    @Test
    public void testDragDropCanvas() {
        driver.get("https://example.com/drawing-app");
        
        WebElement canvas = driver.findElement(By.id("canvas"));
        
        // Draw a line by dragging across canvas
        actions.moveToElement(canvas, 10, 10)  // Start position
               .clickAndHold()
               .moveByOffset(100, 100)          // End position
               .release()
               .perform();
    }
}
```

### 3. Context Menu Actions

```java
public class ContextMenuActions {
    private WebDriver driver;
    private Actions actions;
    
    @Test
    public void testRightClickMenu() {
        driver.get("https://example.com/context-menu");
        
        WebElement targetElement = driver.findElement(By.id("right-click-area"));
        
        // Right-click to open context menu
        actions.contextClick(targetElement).perform();
        
        // Wait for menu to appear
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(5));
        WebElement menu = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("context-menu")));
        
        // Click on menu option
        WebElement copyOption = menu.findElement(By.xpath(".//span[text()='Copy']"));
        copyOption.click();
        
        // Verify action was performed
        WebElement statusMessage = driver.findElement(By.id("status"));
        Assert.assertEquals("Item copied", statusMessage.getText());
    }
}
```

### 4. Hover Effects and Tooltips

```java
public class HoverActions {
    private WebDriver driver;
    private Actions actions;
    
    @Test
    public void testHoverTooltip() {
        driver.get("https://example.com/tooltips");
        
        WebElement hoverElement = driver.findElement(By.id("hover-me"));
        
        // Hover over element
        actions.moveToElement(hoverElement).perform();
        
        // Wait for tooltip to appear
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(5));
        WebElement tooltip = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("tooltip")));
        
        // Verify tooltip content
        Assert.assertTrue(tooltip.isDisplayed());
        Assert.assertEquals("This is a tooltip", tooltip.getText());
    }
    
    @Test
    public void testDropdownOnHover() {
        driver.get("https://example.com/hover-dropdown");
        
        WebElement menuItem = driver.findElement(By.id("menu-item"));
        
        // Hover to open dropdown
        actions.moveToElement(menuItem).perform();
        
        // Wait for dropdown to appear
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(5));
        WebElement dropdown = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("dropdown-menu")));
        
        // Click on dropdown option
        WebElement subMenuItem = dropdown.findElement(By.linkText("Sub Menu Item"));
        actions.moveToElement(subMenuItem).click().perform();
    }
}
```

## Advanced Actions Patterns

### 1. Action Builder Pattern

**What is Action Builder Pattern?**
A custom wrapper around Selenium's Actions class that stores actions in a sequence and executes them when needed, instead of executing immediately.

**Why use it?**
- Better readability for complex action sequences
- Reusable action workflows
- Execute multiple actions at once with better control

```java
public class ActionBuilder {
    private Actions actions;
    private List<Action> actionSequence;
    
    public ActionBuilder(WebDriver driver) {
        this.actions = new Actions(driver);
        this.actionSequence = new ArrayList<>();
    }
    
    public ActionBuilder click(WebElement element) {
        actionSequence.add(actions.click(element).build());
        return this;
    }
    
    public ActionBuilder hover(WebElement element) {
        actionSequence.add(actions.moveToElement(element).build());
        return this;
    }
    
    public ActionBuilder sendKeys(String text) {
        actionSequence.add(actions.sendKeys(text).build());
        return this;
    }
    
    public ActionBuilder pause(int milliseconds) {
        actionSequence.add(actions.pause(Duration.ofMillis(milliseconds)).build());
        return this;
    }
    
    public void execute() {
        for (Action action : actionSequence) {
            action.perform();
        }
        actionSequence.clear();
    }
}

// Usage
ActionBuilder builder = new ActionBuilder(driver);
builder.click(element1)
       .pause(1000)
       .hover(element2)
       .sendKeys("text")
       .execute();
```

### 2. Cross-Platform Actions

**What is Cross-Platform Actions?**
Handling keyboard shortcuts that differ between operating systems (Mac uses Cmd, Windows/Linux use Ctrl).

**Why needed?**
Different OS use different modifier keys for the same shortcuts (Copy: Cmd+C on Mac, Ctrl+C on Windows).

```java
public class CrossPlatformActions {
    private Actions actions;
    private String osName;
    
    public CrossPlatformActions(WebDriver driver) {
        this.actions = new Actions(driver);
        this.osName = System.getProperty("os.name").toLowerCase();
    }
    
    // Copy that works on both Mac and Windows
    public void copy() {
        if (osName.contains("mac")) {
            actions.keyDown(Keys.COMMAND).sendKeys("c").keyUp(Keys.COMMAND).perform();
        } else {
            actions.keyDown(Keys.CONTROL).sendKeys("c").keyUp(Keys.CONTROL).perform();
        }
    }
    
    // Paste that works on both Mac and Windows
    public void paste() {
        if (osName.contains("mac")) {
            actions.keyDown(Keys.COMMAND).sendKeys("v").keyUp(Keys.COMMAND).perform();
        } else {
            actions.keyDown(Keys.CONTROL).sendKeys("v").keyUp(Keys.CONTROL).perform();
        }
    }
    
    // Select all that works on both platforms
    public void selectAll() {
        if (osName.contains("mac")) {
            actions.keyDown(Keys.COMMAND).sendKeys("a").keyUp(Keys.COMMAND).perform();
        } else {
            actions.keyDown(Keys.CONTROL).sendKeys("a").keyUp(Keys.CONTROL).perform();
        }
    }
}
```

## Common Keys Reference

```java
// Special Keys
Keys.ENTER          // Enter key
Keys.TAB            // Tab key
Keys.ESCAPE         // Escape key
Keys.SPACE          // Space bar
Keys.BACK_SPACE     // Backspace
Keys.DELETE         // Delete key

// Arrow Keys
Keys.ARROW_UP       // Up arrow
Keys.ARROW_DOWN     // Down arrow
Keys.ARROW_LEFT     // Left arrow
Keys.ARROW_RIGHT    // Right arrow

// Function Keys
Keys.F1, Keys.F2... Keys.F12  // Function keys

// Modifier Keys
Keys.CONTROL        // Ctrl key
Keys.SHIFT          // Shift key
Keys.ALT            // Alt key
Keys.COMMAND        // Cmd key (Mac)

// Navigation Keys
Keys.HOME           // Home key
Keys.END            // End key
Keys.PAGE_UP        // Page Up
Keys.PAGE_DOWN      // Page Down

// Number Pad
Keys.NUMPAD0...Keys.NUMPAD9  // Numpad numbers
Keys.ADD            // Numpad +
Keys.SUBTRACT       // Numpad -
Keys.MULTIPLY       // Numpad *
Keys.DIVIDE         // Numpad /
```

## Best Practices

### 1. Always Call perform()
```java
// WRONG: Actions not executed
actions.click(element);

// CORRECT: Actions executed
actions.click(element).perform();
```

### 2. Chain Actions for Better Performance
```java
// LESS EFFICIENT: Multiple perform() calls
actions.moveToElement(element1).perform();
actions.click().perform();
actions.sendKeys("text").perform();

// MORE EFFICIENT: Single perform() call
actions.moveToElement(element1)
       .click()
       .sendKeys("text")
       .perform();
```

### 3. Add Waits for Dynamic Content
```java
public void hoverAndWaitForTooltip(WebElement element) {
    // Hover over element
    actions.moveToElement(element).perform();
    
    // Wait for tooltip to appear
    WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(5));
    wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("tooltip")));
}
```

### 4. Handle Browser Differences
```java
public void browserSpecificDragDrop(WebElement source, WebElement target) {
    String browserName = ((RemoteWebDriver) driver).getCapabilities().getBrowserName();
    
    if (browserName.equalsIgnoreCase("safari")) {
        // Safari needs different approach
        dragDropWithJavaScript(source, target);
    } else {
        // Standard approach for other browsers
        actions.dragAndDrop(source, target).perform();
    }
}
```

## Troubleshooting Common Issues

### 1. Element Not Interactable
```java
// Solution: Scroll to element first
public void scrollAndClick(WebElement element) {
    ((JavascriptExecutor) driver).executeScript("arguments[0].scrollIntoView(true);", element);
    actions.moveToElement(element).click().perform();
}
```

### 2. Hover Not Working
```java
// Solution: Move to element center explicitly
public void reliableHover(WebElement element) {
    actions.moveToElement(element, element.getSize().width/2, element.getSize().height/2)
           .perform();
}
```

### 3. Key Combinations Not Working
```java
// Solution: Add small pauses
public void reliableKeyCombo() {
    actions.keyDown(Keys.CONTROL)
           .pause(Duration.ofMillis(100))
           .sendKeys("c")
           .pause(Duration.ofMillis(100))
           .keyUp(Keys.CONTROL)
           .perform();
}
```

## Key Points to Remember

1. **Always call `.perform()`** to execute actions
   - **Why:** Actions class uses builder pattern - methods only build actions, `perform()` executes them

2. **Chain actions** for better performance  
   - **Why:** Single `perform()` sends all actions as one command, reducing network overhead and ensuring sequential execution

3. **Use waits** for dynamic content
   - **Why:** Actions often trigger asynchronous JavaScript (animations, AJAX) that needs time to complete

4. **Handle cross-platform** differences (Cmd vs Ctrl)
   - **Why:** Mac uses Command key where Windows/Linux use Control key for shortcuts

5. **Test hover actions** carefully - they're sensitive
   - **Why:** Hover depends on precise mouse positioning and timing; small changes in layout can break hover effects

6. **Scroll elements into view** before interaction
   - **Why:** Browsers can't interact with elements outside the viewport or hidden behind other elements

7. **Add small pauses** for complex key combinations
   - **Why:** Applications need time to process key events, especially modifier keys, to avoid missing combinations

8. **Verify actions** completed successfully
   - **Why:** Actions can silently fail due to timing, element state, or browser differences - always verify the expected result occurred

Mouse and Keyboard Actions provide powerful capabilities for **realistic user simulation** and **comprehensive test coverage** in web automation testing.
