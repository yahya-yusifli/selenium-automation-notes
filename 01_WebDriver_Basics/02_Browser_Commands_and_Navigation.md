
## 02 – Browser Commands and Navigation


---

**1. Opening a URL with `.get()`**
```java
driver.get("https://example.com");
```
Loads the specified URL and waits for the page to finish loading.

---

**2. Getting Page Title**
```java
String title = driver.getTitle();
System.out.println("Page Title: " + title);
```
Retrieves the title of the current web page.

---

**3. Getting Current URL**
```java
String url = driver.getCurrentUrl();
System.out.println("Current URL: " + url);
```
Retrieves the full URL of the current web page.

---

**4. Navigating to Another URL**
```java
driver.navigate().to("https://example.com/login");
```
An alternative to `.get()` for loading a new URL.

---

**5. Navigating Back and Forward**
```java
driver.navigate().back(); // Go to previous page
```
```java
driver.navigate().forward(); // Go to next page
```

---

**6. Refreshing the Page**
```java
driver.navigate().refresh();
```
Reloads the current page.

---

**7. Maximizing the Browser Window**
```java
driver.manage().window().maximize();
```
Enlarges the browser to full screen.

---

**8. Closing and Quitting**

**Close Current Window**
```java
driver.close();
```
Closes the currently focused window.

**Quit All Windows**
```java
driver.quit();
```
Closes all windows and ends the WebDriver session.

---

**Summary Table**

| Command | Description |
|---------|-------------|
| `get(url)` | Opens specified URL |
| `getTitle()` | Gets title of the page |
| `getCurrentUrl()` | Returns the current page URL |
| `navigate().to(url)` | Navigates to a different URL |
| `navigate().back()` | Goes back to the previous page |
| `navigate().forward()` | Goes forward in browser history |
| `navigate().refresh()` | Refreshes the current page |
| `manage().window().maximize()` | Maximizes the browser window |
| `close()` | Closes the current browser window |
| `quit()` | Closes all browser windows and ends session |

