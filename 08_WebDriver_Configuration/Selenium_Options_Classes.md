# Selenium Options Classes (ChromeOptions, FirefoxOptions, EdgeOptions, SafariOptions)

This note explains in detail the **Options classes** in Selenium WebDriver.

---

## What Are Options Classes?

In Selenium, **Options** classes allow you to customize and configure how the browser starts and behaves during automation runs.

For each browser, Selenium provides a specific class:

* `ChromeOptions` → for Google Chrome
* `FirefoxOptions` → for Mozilla Firefox
* `EdgeOptions` → for Microsoft Edge
* `SafariOptions` → for Apple Safari

These classes let you:

* Set browser preferences
* Add custom arguments
* Define experimental features
* Attach capabilities
* Handle certificates and proxies

---

## ChromeOptions (Detailed)

### Import and Setup

```java
import org.openqa.selenium.chrome.ChromeOptions;

ChromeOptions options = new ChromeOptions();
```

### Common Uses

1. **Add Arguments**

```java
options.addArguments("--start-maximized");
options.addArguments("--incognito");
```

2. **Set Experimental Options**

```java
options.setExperimentalOption("excludeSwitches", new String[]{"enable-automation"});
```

3. **Set Binary Path** (if Chrome is in a custom location)

```java
options.setBinary("/path/to/chrome");
```

4. **Attach Capabilities**

```java
import org.openqa.selenium.remote.CapabilityType;

options.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true);
options.setCapability("proxy", proxy); // Proxy must be created separately
```

5. **Handle Insecure Certificates**

```java
options.setAcceptInsecureCerts(true);
```

6. **Headless Mode (No UI)**

```java
options.addArguments("--headless=new");
```

7. **Disable Extensions**

```java
options.addArguments("--disable-extensions");
```

8. **Use a Custom User Profile**

```java
options.addArguments("user-data-dir=/path/to/your/custom/profile");
```

9. **Mobile Emulation**

```java
Map<String, String> mobileEmulation = new HashMap<>();
mobileEmulation.put("deviceName", "Nexus 5");
options.setExperimentalOption("mobileEmulation", mobileEmulation);
```

### Passing Options to Driver

```java
WebDriver driver = new ChromeDriver(options);
```

---

## FirefoxOptions

### Setup

```java
import org.openqa.selenium.firefox.FirefoxOptions;

FirefoxOptions options = new FirefoxOptions();
options.addArguments("-private");
```

### Accept Insecure Certificates

```java
options.setAcceptInsecureCerts(true);
```

### Headless

```java
options.addArguments("-headless");
```

---

## EdgeOptions

### Setup

```java
import org.openqa.selenium.edge.EdgeOptions;

EdgeOptions options = new EdgeOptions();
options.addArguments("--start-maximized");
```

### Accept Insecure Certificates

```java
options.setAcceptInsecureCerts(true);
```

---

## SafariOptions

### Setup

```java
import org.openqa.selenium.safari.SafariOptions;

SafariOptions options = new SafariOptions();
```

Safari has fewer configurable options compared to Chrome/Firefox.

---

## Important Notes

* **Capabilities**: Before Selenium 4, `DesiredCapabilities` were used. Now, most capabilities are set directly via the `Options` classes.
* **Combining Options and Capabilities**: You can still merge them if needed using `merge()`.
* **Browser Version**: Always ensure the version of your WebDriver (chromedriver, geckodriver, etc.) matches your local browser version.
* **Cross-browser Automation**: While the patterns are similar, each browser has unique flags, so always refer to official documentation.

---

