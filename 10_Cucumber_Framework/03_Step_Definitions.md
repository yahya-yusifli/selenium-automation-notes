# Step Definitions in Cucumber

**what are step definitions?**

step definitions are java methods that connect each gherkin step in a `.feature` file to automation code. they are annotated using `@given`, `@when`, `@then`, `@and`, or `@but` to define the behavior of each step.

---

**basic structure**

```java
@Given("user is on login page")
public void user_is_on_login_page() {
    // selenium code to open login page
}
```

---

**parameterized steps**

```gherkin
scenario: login with parameters
  given user logs in with "admin" and "admin123"
```

```java
@Given("user logs in with {string} and {string}")
public void login_with_credentials(String username, String password) {
    // use parameters in test logic
}
```

---

**regular expressions in step definitions**

```java
@When("^user enters username (.+) and password (.+)$")
public void user_enters_username_and_password(String username, String password) {
    // dynamic input handling
}
```

---

**best practices**

* use clear and consistent wording between steps and definitions
* reuse common steps across scenarios
* avoid logic-heavy methods; delegate actions to page object classes
* store locators in separate page classes (pom)
* keep each step focused and short

---

**summary**

step definitions are the backbone of cucumber tests, allowing you to automate gherkin steps using java code. they should remain clean, readable, and reusable.
