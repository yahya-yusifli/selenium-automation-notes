# 01_WebDriver_Basics

## Selenium Introduction
- What is Selenium?
- Advantages of Selenium for automation.
- Selenium Suite Components: WebDriver, IDE, Grid.

## Installing Java and Selenium
- Install Java JDK
- Setup Environment Variables (JAVA_HOME, PATH)
- Install IntelliJ IDEA / Eclipse
- Install Maven (optional but recommended)
- Download Selenium WebDriver JAR files or use Maven dependencies.

## Setting up and Launching Browser
- Setting up ChromeDriver
- Launching a browser session with `WebDriver driver = new ChromeDriver();`
- Navigating to a URL with `driver.get("url")`
- Browser commands: maximize, minimize, refresh, back, forward.

# WebDriver Interface and Browser Drivers in Selenium

## 1. What is Interface in Java?

- An **interface** is a collection of related methods with empty bodies (no implementation).
- It is the **responsibility of a class** to **implement** the methods declared in the Interface.
- When a class agrees to implement an interface, it **must provide implementation** (method bodies) for **all the defined methods**.
- **In simple terms:**  
  ➔ An Interface **enforces a contract** that the class must follow.

---

## 2. What is WebDriver Interface?

- **WebDriver** is an **interface** that provides a set of browser automation methods with **empty bodies** (abstract methods).
- **Browser-specific classes** like:
  - `ChromeDriver`
  - `FirefoxDriver`
  - `EdgeDriver`
  - `SafariDriver`
  
  **implement** the `WebDriver` Interface and provide their **own implementations** of the methods.

---

# How WebDriver, Browser Drivers, and Browser Work Together

## 1. WebDriver Client

- The WebDriver client translates the commands from your Selenium script into **HTTP requests** following the **W3C WebDriver Protocol**.

### Why W3C WebDriver Protocol?
- All modern browsers (Chrome, Firefox, Safari, Edge) **natively support the W3C protocol**.
- It ensures **consistent behavior** across different browsers.

---

## 2. Browser Driver

- **What is a Browser Driver?**
  - Each browser (Chrome, Firefox, Safari, etc.) has its own dedicated **driver program**.
  - This driver **acts as a translator** between WebDriver protocol (HTTP requests) and the actual browser.
  
### How it works:
1. Your test script sends **HTTP commands** to the browser driver.
2. The **browser driver** translates those commands into native actions for the browser.
3. The browser **executes the commands** (open page, click button, fill form, etc.).
4. The browser sends a **response** back to the browser driver.
5. The browser driver **sends the response** back to your WebDriver client (your Selenium script).

---

# Creating Driver Objects

## 1. Creating a ChromeDriver Object

```java
ChromeDriver driver = new ChromeDriver();
```
- `driver` object has access to **all** the methods of the `ChromeDriver` class.

---

## 2. Creating a WebDriver Reference with ChromeDriver

```java
WebDriver driver = new ChromeDriver();
```
- `driver` object has access to only the **methods declared in the WebDriver interface**.
- Even though the actual object is `ChromeDriver`, you interact with it through the **WebDriver interface reference**.

---

# Summary

| Topic | Explanation |
| --- | --- |
| Interface in Java | Defines abstract methods that must be implemented by classes |
| WebDriver Interface | Defines browser automation methods |
| Browser Drivers | Translate WebDriver commands to real browser actions |
| Object Creation | Create class objects to access methods |


