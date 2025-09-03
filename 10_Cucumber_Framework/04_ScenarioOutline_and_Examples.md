## Scenario Outline

**what is scenario outline?**

scenario outline is a gherkin keyword that allows you to run the same scenario multiple times with different sets of test data. it is useful for data-driven testing.

---

**why use scenario outline?**

* to avoid repeating the same scenario multiple times
* to improve readability and maintainability
* to test the same steps with different inputs and expected outputs

---

**syntax**

```gherkin
scenario outline: scenario title
  given some precondition
  when action is performed with <input1>
  then the outcome should be <result>

examples:
  | input1 | result  |
  | A      | output1 |
  | B      | output2 |
```

---

**example feature file**

```gherkin
feature: login feature

  scenario outline: login with different credentials
    given user is on the login page
    when user enters username "<username>" and password "<password>"
    then login result should be "<result>"

    examples:
      | username | password | result  |
      | admin    | admin123 | success |
      | test     | wrong    | failure |
```

---

**step definition for scenario outline**

```java
@When("user enters username \"{string}\" and password \"{string}\")
public void user_enters_credentials(String username, String password) {
    driver.findElement(By.id("username")).sendKeys(username);
    driver.findElement(By.id("password")).sendKeys(password);
    driver.findElement(By.id("loginBtn")).click();
}

@Then("login result should be \"{string}\")
public void login_result_should_be(String expectedResult) {
    WebElement resultText = driver.findElement(By.id("result"));
    Assert.assertEquals(resultText.getText(), expectedResult);
}
```

---

**best practices**

* keep examples table simple and aligned
* do not hardcode test data inside step definitions
* use clear and meaningful example headers
* combine with tags to organize execution
