# Alert Handling in Selenium

## Accepting an Alert

```java
driver.switchTo().alert().accept();
```
This command switches the WebDriver’s focus to the active alert popup and accepts it (equivalent to clicking "OK").

## Dismissing an Alert

```java
driver.switchTo().alert().dismiss();
```
Dismisses the alert (equivalent to clicking "Cancel" or closing the alert).

## Getting Alert Text

```java
String alertText = driver.switchTo().alert().getText();
System.out.println(alertText);
```
Retrieves and prints the text message from the alert.

## Sending Input to Alert

```java
driver.switchTo().alert().sendKeys("input text");
```
Sends text input to a prompt alert (if supported).

