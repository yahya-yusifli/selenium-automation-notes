# Keyword Driven Framework

## What is Keyword Driven Framework?

A keyword driven framework is a test automation approach where **test actions are represented by keywords** stored in external files. Each keyword corresponds to a specific function in the code.

**Simple Example:**
- Keyword: `launchBrowser` → Function: Opens browser
- Keyword: `enterText` → Function: Types text in field
- Keyword: `clickButton` → Function: Clicks button

## How It Works

### Test Data File (Excel/CSV)
| Keyword | Object | TestData |
|---------|--------|----------|
| launchBrowser | chrome | |
| navigateToURL | | https://example.com |
| enterText | username | testuser |
| enterText | password | testpass |
| clickButton | loginButton | |
| verifyText | welcomeMessage | Welcome |
| closeBrowser | | |

### Keyword Implementation
```java
public class KeywordEngine {
    private WebDriver driver;
    
    public void executeKeyword(String keyword, String object, String testData) {
        switch (keyword.toLowerCase()) {
            case "launchbrowser":
                launchBrowser(object);
                break;
            case "navigatetourl":
                navigateToURL(testData);
                break;
            case "entertext":
                enterText(object, testData);
                break;
            case "clickbutton":
                clickButton(object);
                break;
            case "closebrowser":
                closeBrowser();
                break;
        }
    }
    
    private void launchBrowser(String browserName) {
        if (browserName.equals("chrome")) {
            driver = new ChromeDriver();
        }
    }
    
    private void enterText(String elementName, String text) {
        WebElement element = getElement(elementName);
        element.sendKeys(text);
    }
    
    private void clickButton(String elementName) {
        WebElement element = getElement(elementName);
        element.click();
    }
}
```

## Key Components

### 1. Keywords (Actions)
Common keywords in framework:
```java
launchBrowser(browserType)
navigateToURL(url)
enterText(element, text)
clickButton(element)
selectDropdown(element, value)
verifyText(element, expectedText)
waitForElement(element)
takeScreenshot()
closeBrowser()
```

### 2. Object Repository
```properties
# elements.properties
username=id:username
password=id:password
loginBtn=xpath://button[@type='submit']
welcomeMessage=id:welcome
```

### 3. Test Execution Engine
```java
public class TestExecutionEngine {
    private KeywordEngine keywordEngine;
    
    public void executeTestCase(String testCaseFile) {
        List<String[]> testSteps = readTestData(testCaseFile);
        keywordEngine = new KeywordEngine();
        
        for (String[] step : testSteps) {
            String keyword = step[0];
            String object = step[1];
            String testData = step[2];
            
            keywordEngine.executeKeyword(keyword, object, testData);
        }
    }
}
```

## Framework Structure
```
KeywordFramework/
├── src/main/java/
│   ├── keywords/KeywordEngine.java
│   ├── utils/ExcelUtils.java
│   └── engine/TestExecutionEngine.java
├── src/test/resources/
│   ├── testdata/LoginTest.xlsx
│   └── objects/elements.properties
└── src/test/java/TestRunner.java
```

## Complete Example

### Test Data (LoginTest.xlsx)
```
Step | Keyword      | Object        | TestData
1    | launchBrowser| chrome        |
2    | navigateToURL|               | https://app.com/login
3    | enterText    | username      | admin
4    | enterText    | password      | admin123
5    | clickButton  | loginBtn      |
6    | verifyText   | welcomeMsg    | Welcome Admin
7    | closeBrowser |               |
```

### Enhanced Keyword Engine
```java
public class AdvancedKeywordEngine {
    private WebDriver driver;
    private WebDriverWait wait;
    
    public void executeKeyword(String keyword, String object, String testData) {
        try {
            switch (keyword.toLowerCase()) {
                case "launchbrowser":
                    launchBrowser(object);
                    break;
                case "navigatetourl":
                    driver.get(testData);
                    break;
                case "entertext":
                    enterText(object, testData);
                    break;
                case "clickbutton":
                    clickElement(object);
                    break;
                case "verifytext":
                    verifyText(object, testData);
                    break;
                case "closebrowser":
                    driver.quit();
                    break;
            }
            System.out.println("PASS: " + keyword);
        } catch (Exception e) {
            System.out.println("FAIL: " + keyword + " - " + e.getMessage());
            takeScreenshot();
        }
    }
    
    private void launchBrowser(String browserName) {
        switch (browserName.toLowerCase()) {
            case "chrome":
                driver = new ChromeDriver();
                break;
            case "firefox":
                driver = new FirefoxDriver();
                break;
        }
        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
        driver.manage().window().maximize();
    }
    
    private void enterText(String elementName, String text) {
        WebElement element = getElement(elementName);
        element.clear();
        element.sendKeys(text);
    }
    
    private void clickElement(String elementName) {
        WebElement element = getElement(elementName);
        wait.until(ExpectedConditions.elementToBeClickable(element)).click();
    }
    
    private void verifyText(String elementName, String expectedText) {
        WebElement element = getElement(elementName);
        Assert.assertEquals(element.getText(), expectedText);
    }
    
    private WebElement getElement(String elementName) {
        By locator = ObjectRepository.getLocator(elementName);
        return wait.until(ExpectedConditions.presenceOfElementLocated(locator));
    }
    
    private void takeScreenshot() {
        // Screenshot logic
    }
}
```

### Test Runner
```java
public class KeywordTestRunner {
    
    @Test
    public void runLoginTest() {
        TestExecutionEngine engine = new TestExecutionEngine();
        engine.executeTestCase("testdata/LoginTest.xlsx");
    }
    
    @Test
    public void runRegistrationTest() {
        TestExecutionEngine engine = new TestExecutionEngine();
        engine.executeTestCase("testdata/RegistrationTest.xlsx");
    }
}
```

## Advantages

1. **Non-technical friendly** - Business analysts can write tests
2. **High reusability** - Same keywords used across tests
3. **Easy maintenance** - Change code once, updates all tests
4. **Readable tests** - Plain English keywords
5. **Separation** - Test logic separate from test data

## Disadvantages

1. **Initial setup time** - Takes time to build framework
2. **Limited flexibility** - Hard to handle complex scenarios
3. **Performance overhead** - Interpretation layer adds delay
4. **Debugging difficulty** - Harder to troubleshoot failures
5. **Many keywords needed** - Large keyword library required

## When to Use

**Use Keyword Driven Framework When:**
- Team has non-technical members writing tests
- Need high reusability of test components
- Simple, repetitive test scenarios
- Long-term maintenance is important
- Business users want to contribute to testing

**Avoid When:**
- Complex test logic required
- Performance is critical
- Team is purely technical
- Quick development cycles needed
- Tests change frequently

## Best Practices

1. **Keep keywords simple** - One action per keyword
2. **Use descriptive names** - `clickLoginButton` not `click1`
3. **Handle errors gracefully** - Log failures with screenshots
4. **Maintain object repository** - Centralize element locators
5. **Version control test data** - Track changes in test files
6. **Add logging** - Track test execution steps
7. **Regular maintenance** - Update keywords as app changes

## Key Points

- **Keyword = Action** - Each keyword represents one test action
- **External test data** - Keywords stored in Excel/CSV files
- **Interpretation layer** - Engine reads keywords and executes functions
- **High maintenance overhead** - Requires dedicated framework maintenance
- **Best for simple scenarios** - Complex logic is difficult to implement
- **Team skill consideration** - Works best with mixed technical/non-technical teams

Keyword Driven Framework is excellent for teams needing **maintainable**, **reusable** automation where **non-technical members** contribute to test creation.
