## JavaScriptExecutor in selenium

`javascriptexecutor` is an interface in selenium webdriver that allows you to run javascript code directly in the browser from java automation scripts. it is helpful when standard webdriver methods cannot interact with certain elements or when javascript-only operations are needed.

---

**why use javascriptexecutor?**
- interact with elements webdriver can’t handle easily (e.g., hidden, shadow dom)
- perform scroll operations
- modify or read attributes directly
- trigger js-based events
- bypass some browser limitations
- improve speed where webdriver is unreliable

---

**when to use javascriptexecutor**

**1. elementclickinterceptedexception**
```java
js.executescript("arguments[0].click();", element);
```
use when `.click()` fails due to overlays or popups blocking the element.

**2. element in dom but not visible**
```java
js.executescript("arguments[0].click();", element);
```
use when an element has `display: none` or is only visible on hover.

**3. scroll to an element**
```java
js.executescript("arguments[0].scrollintoview(true);", element);
```
use to make an element visible before interacting.

**4. speed and flakiness fixes**
javascript can be faster and more reliable in js-heavy applications.

**5. set value in field blocking sendkeys()**
```java
js.executescript("arguments[0].value='myvalue';", input);
```

---

**basic syntax**
```java
javascriptexecutor js = (javascriptexecutor) driver;
js.executescript("your javascript code here");
```

---

**common use cases**

**execute javascript**
```java
js.executescript("alert('hello world');");
```

**return a value**
```java
string pagetitle = (string) js.executescript("return document.title;");
```

**click an element**
```java
webelement button = driver.findelement(by.id("submit"));
js.executescript("arguments[0].click();", button);
```

**set value to input**
```java
webelement input = driver.findelement(by.id("username"));
js.executescript("arguments[0].value='myusername';", input);
```

**scroll the page**
```java
js.executescript("window.scrollby(0,500);");
js.executescript("window.scrollto(0, document.body.scrollheight);");
js.executescript("arguments[0].scrollintoview(true);", element);
```

**highlight an element**
```java
js.executescript("arguments[0].style.border='3px solid red';", element);
```

**retrieve element attributes**
```java
string innertext = (string) js.executescript("return arguments[0].innertext;", element);
```

---

**best practices**
- use javascriptexecutor only when webdriver’s native methods fail
- clearly comment why js is used to improve maintainability
- avoid overuse to keep code clean and test-friendly

let me know if you’d like to wrap this into a `javascriptactions` utility class for reuse in your framework.
