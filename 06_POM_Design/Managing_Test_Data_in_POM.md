# Managing Test Data in Page Object Model (POM)

This document outlines how to manage test data effectively in a Selenium automation framework using the Page Object Model (POM).

---

## Why Test Data Management Matters

- Keeps test logic and test data separate
- Improves readability, maintainability, and scalability
- Enables data-driven testing

---

## 1. Externalizing Test Data

### a. Using Properties File

**testdata.properties:**
```properties
username=admin
password=admin123
```

**Usage in Java:**
```java
Properties prop = new Properties();
FileInputStream fis = new FileInputStream("src/test/resources/testdata.properties");
prop.load(fis);

String username = prop.getProperty("username");
```

---

### b. Using Excel File (Apache POI)

**Sample Code to Read Excel:**
```java
FileInputStream fis = new FileInputStream("src/test/resources/data.xlsx");
Workbook wb = new XSSFWorkbook(fis);
Sheet sheet = wb.getSheet("LoginData");
String username = sheet.getRow(1).getCell(0).getStringCellValue();
```

---

### c. Using JSON File (via Jackson or Gson)

**testdata.json:**
```json
{
  "username": "admin",
  "password": "admin123"
}
```

**Sample Code Using Jackson:**
```java
ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(new File("src/test/resources/testdata.json"));
String username = node.get("username").asText();
```

---

## 2. Using @DataProvider in TestNG

```java
@DataProvider(name = "loginData")
public Object[][] getLoginData() {
    return new Object[][] {
        {"admin", "admin123"},
        {"user", "userpass"}
    };
}

@Test(dataProvider = "loginData")
public void testLogin(String username, String password) {
    loginPage.login(username, password);
    // assertions here
}
```

---

## 3. Environment-Based Data

You can maintain different test data for different environments (e.g., QA, UAT, PROD):

**Structure:**
```
src/test/resources/config/
├── qa.properties
├── uat.properties
├── prod.properties
```

**Usage:**
```java
String env = System.getProperty("env"); // -Denv=qa
FileInputStream fis = new FileInputStream("src/test/resources/config/" + env + ".properties");
```

---

## 4. Page Classes Should Not Store Static Test Data

Keep page classes focused on **element interaction**, not hardcoded test data.

**Bad:**
```java
public void login() {
    driver.findElement(username).sendKeys("admin");
    driver.findElement(password).sendKeys("admin123");
}
```

**Good:**
```java
public void login(String username, String password) {
    driver.findElement(this.username).sendKeys(username);
    driver.findElement(this.password).sendKeys(password);
}
```

---

## Summary Table

| Technique        | Use Case                               |
|------------------|------------------------------------------|
| Properties File  | Simple static values (credentials, URLs) |
| Excel            | Tabular datasets for many test cases     |
| JSON             | Structured or nested data sets           |
| DataProvider     | Parameterized test methods               |
| Environment Props| Config/data for different environments   |

---

## Best Practices

- Avoid hardcoding values inside tests or page classes.
- Keep test data in one place.
- Match data format to your needs (simple → properties, complex → JSON/Excel).
- Support multi-environment execution.

