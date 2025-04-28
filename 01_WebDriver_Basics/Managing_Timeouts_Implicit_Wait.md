# Managing Timeouts - Implicit Wait

Implicit wait tells WebDriver to poll the DOM for a certain amount of time when trying to find an element.

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
