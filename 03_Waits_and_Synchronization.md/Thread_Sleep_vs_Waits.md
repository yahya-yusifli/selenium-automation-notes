
## Thread.sleep vs Waits

- `Thread.sleep()` pauses execution unconditionally for the specified time (hard wait)
- Waits (implicit, explicit, fluent) only pause until the condition is met (soft wait)
- `Thread.sleep()` wastes time if the element is ready sooner

**Best practice:** avoid `Thread.sleep()` except for debugging

---
