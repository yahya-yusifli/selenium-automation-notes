# Retry Failed Tests Using Listeners

This document explains how to retry failed tests.

## How It Works

- Implement `IRetryAnalyzer` interface.
- Attach it to test methods.

## Example

```java
public class RetryAnalyzer implements IRetryAnalyzer {
    ...
}
```
