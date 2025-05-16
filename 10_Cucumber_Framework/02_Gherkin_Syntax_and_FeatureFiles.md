
# Gherkin Syntax and Feature Files

**Gherkin** is the language used by Cucumber to describe application behavior in plain, readable sentences.

---

**1. What is Gherkin?**

Gherkin is a domain-specific language that enables describing test cases in natural language.  
It acts as the link between business logic and automated test implementation.

---

**2. Basic Structure of a Feature File**

Each feature file starts with the `Feature` keyword and contains one or more `Scenario`s.

```gherkin
Feature: User Login Functionality

  Scenario: Successful login with valid credentials
    Given user is on login page
    When user enters valid username and password
    Then user should be redirected to homepage
```

---

**3. Gherkin Keywords**

| Keyword   | Purpose                                 |
|-----------|-----------------------------------------|
| Feature   | Defines the high-level business feature |
| Scenario  | Defines a single concrete test case     |
| Given     | Describes the initial context           |
| When      | Describes the user action               |
| Then      | Describes the expected outcome          |
| And/But   | Used to add more steps under Given/When/Then |
| Scenario Outline | Template for parameterized testing |
| Examples  | Provides data for Scenario Outline      |

---

**4. Scenario Outline Example**

```gherkin
Scenario Outline: Login with valid and invalid credentials
  Given user is on login page
  When user enters "<username>" and "<password>"
  Then user should see "<message>"

Examples:
  | username        | password | message              |
  | user@example.com| pass123  | Welcome              |
  | user@wrong.com  | wrong    | Invalid credentials  |
```

---

**5. Feature File Best Practices**

- Use meaningful feature and scenario titles
- Keep scenarios short and focused (1 purpose per scenario)
- Reuse step definitions
- Don’t describe UI steps (clicks, paths) in the feature file
- Prefer `Scenario Outline` for testing multiple input combinations

---

**6. Naming and Folder Structure**

Place your `.feature` files under:

```
src/test/resources/features/
```

Each feature file should be named with an underscore and `.feature` extension:
```
Login.feature
Add_Product.feature
Search_Functionality.feature
```

---

**7. Summary**

- Feature files contain business-readable test cases
- Gherkin syntax is composed of Given/When/Then steps
- Cucumber parses `.feature` files and matches steps to Java methods (step definitions)
- Keeping your feature files clean, consistent, and purposeful improves test clarity and collaboration
