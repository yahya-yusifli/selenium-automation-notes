
# Retry Failed Tests Using Listeners in TestNG
## How It Works
To retry failed tests in TestNG:
- Implement the `IRetryAnalyzer` interface.  
- Attach the retry logic to test methods.  
- Optionally integrate with listeners or reporters for better tracking.

This is especially useful when tests fail due to **intermittent issues** like network delays, environmental flakiness, or slow response times.

---

## Step 1: Implement `IRetryAnalyzer`

Create a retry analyzer class:

```java
import org.testng.IRetryAnalyzer;
import org.testng.ITestResult;

public class RetryAnalyzer implements IRetryAnalyzer {

    private int retryCount = 0;
    private static final int maxRetryCount = 2;

    @Override
    public boolean retry(ITestResult result) {
        if (retryCount < maxRetryCount) {
            retryCount++;
            System.out.println("Retrying test: " + result.getName() + ", Attempt: " + (retryCount + 1));
            return true; // retry
        }
        return false; // no more retries
    }
}
```

 **Key points:**
- `maxRetryCount` → how many times to retry a failing test.
- `retry()` → returns `true` to retry, `false` to stop.

---

## Step 2: Attach RetryAnalyzer to Tests

You can attach it directly to individual test methods:

```java
@Test(retryAnalyzer = RetryAnalyzer.class)
public void flakyTest() {
    Assert.assertTrue(new Random().nextBoolean()); // random pass/fail
}
```

 **Tip:** Only use retries on tests you know can fail due to **temporary conditions** (e.g., external services, timeouts).

---

## Step 3: Apply Retry Globally (Optional)

If you want to apply retry logic to **all tests automatically**, you can use a listener.

Create a listener class implementing `IAnnotationTransformer`:

```java
import org.testng.IAnnotationTransformer;
import org.testng.annotations.ITestAnnotation;
import java.lang.reflect.Constructor;
import java.lang.reflect.Method;

public class RetryListener implements IAnnotationTransformer {
    @Override
    public void transform(ITestAnnotation annotation, Class testClass, Constructor testConstructor, Method testMethod) {
        annotation.setRetryAnalyzer(RetryAnalyzer.class);
    }
}
```

Then register it in `testng.xml`:

```xml
<listeners>
    <listener class-name="com.example.RetryListener"/>
</listeners>
```

 **Result:** All your tests will now use the retry logic automatically.

---

## Step 4: Review Retry Results

- TestNG reports (`test-output` folder) will show both original failures and retries.
- You can also extend the logic to log retries in custom reports or take screenshots on failures.

---

## Best Practices

- Keep retry counts low (1-2) to avoid masking real failures.  
- Investigate **why** tests fail before adding retries (don’t cover up bad tests).  
- Combine retries with detailed logging and reporting for better traceability.  
- Document which tests use retry logic and why.

---

