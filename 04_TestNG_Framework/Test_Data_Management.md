# Test Data Management in Selenium

## What is Test Data Management?

Test Data Management is the practice of **separating test data from test code**. Instead of hardcoding values in your tests, you store them externally and feed them to your tests dynamically.

## Why Use Test Data Management?

**Without Test Data Management:**
```java
// BAD: Hardcoded data
@Test
public void loginTest() {
    driver.findElement(By.id("username")).sendKeys("admin");
    driver.findElement(By.id("password")).sendKeys("admin123");
}
```

**With Test Data Management:**
```java
// GOOD: External data
@Test(dataProvider = "loginData")
public void loginTest(String username, String password) {
    driver.findElement(By.id("username")).sendKeys(username);
    driver.findElement(By.id("password")).sendKeys(password);
}
```

**Benefits:**
- **Maintainability**: Change data without touching code
- **Reusability**: Same test with different data
- **Scalability**: Easy to add more test scenarios
- **Team Collaboration**: Non-technical people can manage data

## Data Sources

### 1. Properties Files

**testdata.properties:**
```properties
admin.username=admin
admin.password=admin123
user.username=testuser
user.password=userpass
```

**Usage:**
```java
Properties prop = new Properties();
FileInputStream fis = new FileInputStream("src/test/resources/testdata.properties");
prop.load(fis);

String username = prop.getProperty("admin.username");
String password = prop.getProperty("admin.password");
```

### 2. Excel Files (Apache POI)

**Reading Excel:**
```java
FileInputStream fis = new FileInputStream("src/test/resources/testdata.xlsx");
Workbook workbook = new XSSFWorkbook(fis);
Sheet sheet = workbook.getSheet("LoginData");

String username = sheet.getRow(1).getCell(0).getStringCellValue();
String password = sheet.getRow(1).getCell(1).getStringCellValue();
```

**Excel Data Provider:**
```java
@DataProvider(name = "excelData")
public Object[][] getExcelData() {
    // Read Excel file and return 2D array
    return new Object[][] {
        {"admin", "admin123"},
        {"user", "userpass"}
    };
}
```

### 3. JSON Files

**testdata.json:**
```json
{
  "admin": {
    "username": "admin",
    "password": "admin123"
  },
  "user": {
    "username": "testuser", 
    "password": "userpass"
  }
}
```

**Reading JSON:**
```java
ObjectMapper mapper = new ObjectMapper();
JsonNode root = mapper.readTree(new File("src/test/resources/testdata.json"));
String username = root.get("admin").get("username").asText();
```

### 4. CSV Files

**testdata.csv:**
```csv
username,password,expectedResult
admin,admin123,success
user,userpass,success
invalid,wrong,error
```

**Reading CSV:**
```java
CSVReader reader = new CSVReader(new FileReader("src/test/resources/testdata.csv"));
List<String[]> allData = reader.readAll();
```

## TestNG Data Provider

### Basic Data Provider
```java
@DataProvider(name = "loginData")
public Object[][] getLoginData() {
    return new Object[][] {
        {"admin", "admin123", "success"},
        {"user", "userpass", "success"},
        {"invalid", "wrong", "error"}
    };
}

@Test(dataProvider = "loginData")
public void testLogin(String username, String password, String expected) {
    loginPage.login(username, password);
    
    if (expected.equals("success")) {
        Assert.assertTrue(homePage.isWelcomeMessageDisplayed());
    } else {
        Assert.assertTrue(loginPage.isErrorDisplayed());
    }
}
```

### External File Data Provider
```java
@DataProvider(name = "externalData")
public Object[][] getDataFromFile() {
    // Read from Excel, CSV, or JSON
    return readDataFromExcel("src/test/resources/logindata.xlsx");
}
```

## Environment-Based Data

### Structure
```
src/test/resources/config/
├── qa.properties
├── staging.properties
├── prod.properties
```

### Usage
```java
String env = System.getProperty("env", "qa"); // -Denv=staging
String configFile = "config/" + env + ".properties";

Properties props = new Properties();
props.load(getClass().getResourceAsStream(configFile));

String baseUrl = props.getProperty("base.url");
String username = props.getProperty("admin.username");
```

## Best Practices

### 1. Keep Page Classes Clean
```java
// BAD: Hardcoded data in page class
public void login() {
    usernameField.sendKeys("admin");
    passwordField.sendKeys("admin123");
}

// GOOD: Accept data as parameters
public void login(String username, String password) {
    usernameField.sendKeys(username);
    passwordField.sendKeys(password);
}
```

### 2. Data Organization
```
src/test/resources/
├── testdata/
│   ├── login/
│   │   ├── validUsers.xlsx
│   │   └── invalidUsers.xlsx
│   ├── registration/
│   │   └── userRegistration.csv
│   └── config/
│       ├── qa.properties
│       └── prod.properties
```

### 3. Configuration Manager
```java
public class ConfigManager {
    private static Properties config = new Properties();
    
    static {
        String env = System.getProperty("test.env", "qa");
        loadConfig("config/" + env + ".properties");
    }
    
    public static String get(String key) {
        return config.getProperty(key);
    }
    
    private static void loadConfig(String fileName) {
        try (InputStream is = ConfigManager.class.getResourceAsStream(fileName)) {
            config.load(is);
        } catch (Exception e) {
            throw new RuntimeException("Config load failed", e);
        }
    }
}
```

### 4. Data Factory Pattern
```java
public class TestDataFactory {
    public static UserData getValidUser() {
        return new UserData(
            ConfigManager.get("valid.username"),
            ConfigManager.get("valid.password")
        );
    }
    
    public static UserData getInvalidUser() {
        return new UserData("invalid", "wrong");
    }
}
```

## Complete Example

### Test Data (Excel)
| Username | Password | ExpectedResult |
|----------|----------|----------------|
| admin | admin123 | success |
| user | userpass | success |
| invalid | wrong | error |

### Test Implementation
```java
public class DataDrivenLoginTest {
    private WebDriver driver;
    
    @DataProvider(name = "loginData")
    public Object[][] getLoginData() {
        return ExcelUtils.readExcel("testdata/loginData.xlsx", "Sheet1");
    }
    
    @Test(dataProvider = "loginData")
    public void testLogin(String username, String password, String expected) {
        // Navigate to login page
        driver.get(ConfigManager.get("base.url") + "/login");
        
        // Perform login
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login(username, password);
        
        // Verify result
        if ("success".equals(expected)) {
            HomePage homePage = new HomePage(driver);
            Assert.assertTrue(homePage.isWelcomeMessageDisplayed());
        } else {
            Assert.assertTrue(loginPage.isErrorMessageDisplayed());
        }
    }
}
```

## Key Points

1. **Separate data from code** for better maintenance
2. **Choose right data source** based on team needs (Excel for non-technical, JSON for developers)
3. **Use TestNG DataProvider** for parameterized tests
4. **Organize data by modules** and environments
5. **Keep page classes free** of hardcoded data
6. **Use configuration management** for environment-specific data
7. **Validate data** before using in tests

Test Data Management makes your automation framework **flexible**, **maintainable**, and **scalable**.
