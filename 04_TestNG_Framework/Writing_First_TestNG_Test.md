
# Writing Your First TestNG Test

This guide explains how to write your first TestNG test using the code you’ve been working on, organized and improved for clarity.

---

## Prerequisites

 Ensure you have:
- Java installed (JDK 8+)
- TestNG added to your project (via Maven, Gradle, or IDE plugin)
- IntelliJ IDEA or Eclipse set up for Java + TestNG

---

## Example Code Structure

We’ll improve and clean up your `CarLoan`, `HomeLoan`, and `PersonalLoan` test classes.

---

### 1. CarLoan Test Class

```java
package test;

import org.testng.annotations.*;

public class CarLoan {

    @BeforeSuite
    public void beforeSuite() {
        System.out.println("[BeforeSuite] Setup global resources");
    }

    @AfterSuite
    public void afterSuite() {
        System.out.println("[AfterSuite] Cleanup global resources");
    }

    @BeforeClass
    public void beforeClass() {
        System.out.println("[BeforeClass] Setup before CarLoan tests");
    }

    @AfterClass
    public void afterClass() {
        System.out.println("[AfterClass] Cleanup after CarLoan tests");
    }

    @BeforeMethod
    public void beforeMethod() {
        System.out.println("[BeforeMethod] Preparing test method");
    }

    @AfterMethod
    public void afterMethod() {
        System.out.println("[AfterMethod] Cleaning up test method");
    }

    @Parameters({"URL"})
    @Test(groups = {"Smoke"})
    public void loginCarLoan(String urlName) {
        System.out.println("[Test] loginCarLoan");
        System.out.println("Received URL: " + urlName);
    }

    @Test(timeOut = 4000)
    public void webLoginCarLoan() {
        System.out.println("[Test] webLoginCarLoan");
    }

    @Test
    public void mobileSignInCarLoan() {
        System.out.println("[Test] mobileSignInCarLoan");
    }

    @Test(dependsOnMethods = {"mobileSignInCarLoan"})
    public void loginAPICarLoan() {
        System.out.println("[Test] loginAPICarLoan");
    }
}
```

---

### 2. HomeLoan Test Class

```java
package test;

import org.testng.annotations.*;

public class HomeLoan {

    @Parameters({"URL"})
    @Test(groups = {"Smoke"})
    public void webLoginHomeLoan(String urlName) {
        System.out.println("[Test] webLoginHomeLoan");
        System.out.println("Received URL: " + urlName);
    }

    @Parameters({"URL"})
    @Test
    public void mobileLoginHomeLoan(String urlName) {
        System.out.println("[Test] mobileLoginHomeLoan");
        System.out.println("Received URL: " + urlName);
    }

    @Test
    public void loginAPIHomeLoan() {
        System.out.println("[Test] loginAPIHomeLoan");
    }
}
```

---

### 3. PersonalLoan Test Class

```java
package test;

import org.testng.annotations.*;

public class PersonalLoan {

    @Test
    public void webLoginPersonalLoan() {
        System.out.println("[Test] webLoginPersonalLoan");
    }

    @Test
    public void mobileLoginPersonalLoan() {
        System.out.println("[Test] mobileLoginPersonalLoan");
    }

    @Test
    public void loginAPIPersonalLoan() {
        System.out.println("[Test] loginAPIPersonalLoan");
    }
}
```

---

## Running Tests with testng.xml

Example `testng.xml` file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="Loan Suite">
    <parameter name="URL" value="https://example.com"/>
    <test name="Car Loan Tests">
        <classes>
            <class name="test.CarLoan"/>
        </classes>
    </test>
    <test name="Home Loan Tests">
        <classes>
            <class name="test.HomeLoan"/>
        </classes>
    </test>
    <test name="Personal Loan Tests">
        <classes>
            <class name="test.PersonalLoan"/>
        </classes>
    </test>
</suite>
```

---

## Key Points

- Use `@BeforeSuite`, `@BeforeClass`, `@BeforeMethod` to set up shared resources.  
- Use `@Parameters` to inject external values.  
- Group related tests using `@Test(groups = {...})`.  
- Control test runs with `testng.xml` for flexibility.


