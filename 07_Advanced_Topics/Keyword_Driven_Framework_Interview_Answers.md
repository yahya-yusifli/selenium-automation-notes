# Keyword Driven Framework - Interview Answers

## Question: "What is Keyword Driven Framework?"

### Short Answer:
"A Keyword Driven Framework is a test automation approach where **test actions are represented by keywords** stored in external files like Excel. Each keyword corresponds to a specific function in the code."

### With Example:
"For example, instead of writing code, we write test steps in Excel like:
- `openBrowser | chrome`
- `enterText | username | admin`  
- `clickButton | loginBtn`

The framework reads these keywords and executes the corresponding functions."

## Question: "How does it work?"

### Answer:
"It has **three main components**:

1. **Test Data File** - Excel/CSV with keywords and parameters
2. **Keyword Engine** - Java code that maps keywords to actions
3. **Object Repository** - Stores element locators

The engine reads test data, finds the matching function for each keyword, and executes it."

## Question: "What are the advantages?"

### Answer:
"Main advantages are:
- **Non-technical people** can write tests
- **High reusability** - same keywords across tests
- **Easy maintenance** - change code once, affects all tests
- **Readable test cases** in plain English"

## Question: "What are the disadvantages?"

### Answer:
"Key disadvantages:
- **Time-consuming setup** initially
- **Limited flexibility** for complex scenarios
- **Performance overhead** due to interpretation layer
- **Debugging is harder** compared to direct code"

## Question: "When would you use it?"

### Answer:
"Use it when:
- Team has **non-technical members** writing tests
- Need **long-term maintainable** automation
- **Simple, repetitive** test scenarios
- **Business users** want to contribute to testing

Avoid for **complex test logic** or when **performance is critical**."

## Question: "Can you give a practical example?"

### Answer:
"Sure! For a login test:

**Excel file:**
```
openBrowser | chrome
navigateToURL | https://app.com
enterText | username | admin
enterText | password | 123
clickButton | loginBtn
verifyText | welcome | Welcome
```

**Java code:**
```java
if (keyword.equals("enterText")) {
    driver.findElement(By.id(object)).sendKeys(testData);
}
```

The framework reads Excel, executes matching Java functions."

## Question: "How is it different from Data Driven Framework?"

### Answer:
"**Data Driven** focuses on **different test data** with same test logic.
**Keyword Driven** focuses on **different test actions** using keywords.

**Data Driven:** Same login test with different usernames/passwords
**Keyword Driven:** Different test flows using same keywords (login, registration, etc.)"

## Question: "What challenges did you face implementing it?"

### Answer:
"Main challenges:
- **Initial setup time** - Creating comprehensive keyword library
- **Keyword standardization** - Ensuring team uses consistent naming
- **Error handling** - Managing failures in keyword execution
- **Performance** - Framework overhead compared to direct code
- **Complex scenarios** - Some test logic difficult to represent as keywords"

## Question: "How do you handle error scenarios?"

### Answer:
"Error handling approaches:
- **Try-catch blocks** around each keyword execution
- **Screenshot capture** on failures
- **Detailed logging** for debugging
- **Graceful continuation** - don't stop entire test suite
- **Error reporting** in test results"

```java
try {
    executeKeyword(keyword, object, data);
    log("PASS: " + keyword);
} catch (Exception e) {
    takeScreenshot(keyword);
    log("FAIL: " + keyword + " - " + e.getMessage());
}
```

## Question: "How do you maintain the framework?"

### Answer:
"Maintenance strategies:
- **Regular keyword review** - Remove unused, add new ones
- **Object repository updates** - Keep locators current
- **Keyword library documentation** - Clear usage guidelines
- **Version control** - Track changes in keywords and test data
- **Regular framework testing** - Ensure keywords work correctly"

## Key Points to Remember:

- **Keywords = Actions** stored externally
- **Engine reads and executes** keywords  
- **Good for non-technical** team members
- **High maintenance** but **reusable**
- **Best for simple scenarios**
- Always give **practical examples**
- Mention **real challenges** you faced
- Show understanding of **when to use** vs **when to avoid**

## Quick Reference:

**What:** Keywords represent test actions in external files
**How:** Engine maps keywords to functions and executes them
**When:** Non-technical team, simple scenarios, long-term maintenance
**Pros:** Easy for non-technical, reusable, maintainable
**Cons:** Setup time, limited flexibility, performance overhead
