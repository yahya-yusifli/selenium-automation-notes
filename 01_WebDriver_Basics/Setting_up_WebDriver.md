
# Setting up WebDriver

Setting up WebDriver involves downloading the driver executable (e.g., chromedriver) and configuring it in your project.

```java
System.setProperty("webdriver.chrome.driver", "/path/to/chromedriver");
WebDriver driver = new ChromeDriver();
