
# ChromeOptions Class

## What is ChromeOptions?

`ChromeOptions` is a **Selenium class** that lets you customize and configure how the Chrome browser launches and behaves when running automated tests.  
It allows adding:  
- browser arguments (flags)  
- extensions  
- experimental features  
- preferences  
- headless or incognito mode  
- disabling or enabling specific features

You pass the configured `ChromeOptions` into the ChromeDriver constructor.

## Import

```java
import org.openqa.selenium.chrome.ChromeOptions;
```

## Basic Usage Example

```java
ChromeOptions options = new ChromeOptions();
options.addArguments("--start-maximized");
options.addArguments("--incognito");

WebDriver driver = new ChromeDriver(options);
```

## Common Methods

| Method                                     | Description                                                                                       |
|-------------------------------------------|---------------------------------------------------------------------------------------------------|
| `addArguments(String... args)`             | Adds command-line arguments (e.g., headless, incognito, maximize).                                |
| `addExtensions(File... paths)`             | Adds Chrome extensions by file path.                                                              |
| `setExperimentalOption(String, Object)`    | Sets experimental options like disabling automation banners.                                      |
| `setBinary(String path)`                   | Sets a custom path to the Chrome binary (if not using the system default).                        |
| `setHeadless(boolean headless)`            | Runs Chrome in headless (no-GUI) mode.                                                            |
| `merge(Capabilities)`                      | Merges additional capabilities into the options.                                                  |

## Popular ChromeOptions Configurations

### 1. Start Maximized

```java
options.addArguments("--start-maximized");
```

### 2. Run in Incognito Mode

```java
options.addArguments("--incognito");
```

### 3. Run in Headless Mode

```java
options.addArguments("--headless");
// OR (newer method)
options.setHeadless(true);
```

### 4. Disable Automation Banners

```java
options.setExperimentalOption("excludeSwitches", Arrays.asList("enable-automation"));
```

### 5. Ignore Certificate Errors

```java
options.addArguments("--ignore-certificate-errors");
```

### 6. Add Chrome Extension

```java
options.addExtensions(new File("/path/to/extension.crx"));
```

### 7. Set Custom Download Directory

```java
Map<String, Object> prefs = new HashMap<>();
prefs.put("download.default_directory", "/path/to/download/folder");
options.setExperimentalOption("prefs", prefs);
```

### 8. Disable Pop-up Blocking

```java
options.addArguments("--disable-popup-blocking");
```

## Passing Options to ChromeDriver

```java
WebDriver driver = new ChromeDriver(options);
```

## Best Practices

- Only enable necessary arguments — too many flags can make the browser unstable.
- Always test locally before adding in CI pipelines (especially headless mode).
- Use `WebDriverManager` to manage driver binaries automatically.
- For CI/CD, headless + disable GPU + no-sandbox are common:

```java
options.addArguments("--headless");
options.addArguments("--disable-gpu");
options.addArguments("--no-sandbox");
```

## Official Documentation & Resources

- Selenium Java Docs → [ChromeOptions API](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/chrome/ChromeOptions.html)
- Chrome Command-line Switches → [List](https://peter.sh/experiments/chromium-command-line-switches/)
