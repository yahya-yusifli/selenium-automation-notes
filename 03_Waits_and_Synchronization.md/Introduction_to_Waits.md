# 03_Waits_and_Synchronization

## Introduction to Waits
- Why waits are needed in Selenium automation.
- Page load and dynamic content issues.

## Implicit Wait
- Setting global wait time for all element searches.
- Example: 
  ```java
  driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(5));

