## Cucumber datatables and maps

cucumber allows passing structured tabular data from feature files to step definitions using **datatable**. this is useful for testing forms, tables, or passing multiple values.

---

**1. datatable as list (single column)**

```gherkin
scenario: user submits hobbies
  given the user submits the following hobbies
    | Reading   |
    | Swimming  |
    | Traveling |
```

step definition:

```java
@Given("the user submits the following hobbies")
public void user_submits_hobbies(DataTable dataTable) {
    List<String> hobbies = dataTable.asList();
    for (String hobby : hobbies) {
        System.out.println(hobby);
    }
}
```

---

**2. datatable as list of lists (multiple columns)**

```gherkin
scenario: user submits credentials
  given the user enters the following credentials
    | username | password  |
    | user1    | pass123   |
    | user2    | secret456 |
```

step definition:

```java
@Given("the user enters the following credentials")
public void user_enters_credentials(DataTable dataTable) {
    List<List<String>> data = dataTable.asLists();
    for (List<String> row : data) {
        System.out.println("Username: " + row.get(0) + ", Password: " + row.get(1));
    }
}
```

---

**3. datatable as map (key-value pairs)**

```gherkin
scenario: fill registration form
  given the user fills the form with following data
    | name     | John Doe       |
    | email    | john@email.com |
    | country  | USA            |
```

step definition:

```java
@Given("the user fills the form with following data")
public void fill_form(DataTable dataTable) {
    Map<String, String> formData = dataTable.asMap();
    System.out.println("Name: " + formData.get("name"));
    System.out.println("Email: " + formData.get("email"));
    System.out.println("Country: " + formData.get("country"));
}
```

---

**best practices**

* use table headers clearly to avoid index issues
* prefer maps for readability and semantic access
* combine with scenario outline if data must vary row by row

---

**summary**

* datatables enhance test case readability and flexibility
* step definitions can extract data as list, list of lists, or map
* useful for forms, settings, and structured inputs
