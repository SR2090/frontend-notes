
- **Throttling** limits how many times an event handler can execute over time.
- **Debouncing** ensures that a function is called only once after a burst of events, once things have "settled."

**Mnemonic to Remember:**

- **T**hrottling: **T**icks over time (regular intervals).
- **D**ebouncing: **D**elays until done (only one final call).




Throttling is a technique used to control how many times we allow a function to be executed over time. When a JavaScript function is said to be throttled with a wait time of X milliseconds, it can only be invoked at most once every X milliseconds. The callback is invoked immediately and cannot be invoked again for the rest of the `wait` duration.




## Example
**Throttling Example (Military):**  
Imagine a military surveillance system using radar to track aircraft. Instead of reporting every minor change in position—which would overwhelm the command center—the system sends updates at fixed intervals (e.g., every few seconds). This throttling ensures critical information is communicated without flooding the network.

**Debouncing Example (Military):**  
Consider a missile defense system where sensors detect incoming threats. To avoid false alarms from transient signals (like birds or debris), the system waits until the threat signal remains stable for a defined period before triggering an interception. This debouncing ensures only a sustained threat prompts action.

**Mnemonic to Remember:**

- **Throttling:** **T**icks over time (periodic updates).
- **Debouncing:** **D**elays until steady (only final, confirmed signal).