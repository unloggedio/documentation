# What do we track?

Unlogged tracks a few things from the plugin. This is important for us to improve the developer experience and release better products.

Here are a few things we track.

## **Quick Navigation**
- [Computer Hostname](#computer-hostname)
- [SDK Connection](#sdk-connection)
- [Method Invocation](#method-invocation)
- [SDK Responses](#sdk-responses)
- [Test Case Generation](#test-case-generation)
- [Replay Features](#replay-features)
- [Mock Management](#mock-management)
- [Replay Status Insights](#replay-status-insights)
- [Privacy Assurance](#privacy-assurance)


### **Computer Hostname**
- **What We Track:** Your computer's hostname.
- **Why It Matters:** This helps us gauge the user count and identify where users might encounter issues.

### **SDK Connection**
- **Event Logging:** Initiation of the application with Unlogged SDK.
- **Purpose:** To confirm your successful progression from installation to application startup.

### **Method Invocation**
- **Focus:** Name of the method invoked.
- **Note:** Rest assured, we **do not track** the method's input variables or its return values.

### **SDK Responses**
- **Two Key Events:**
  1. **SDK Response (Normal):** Logged when methods return the expected object smoothly.
  2. **SDK Response (Exception):** Tracked if a method fails or returns an exception.

### **Test Case Generation**
- **Tracking Instance:** Generation of unit tests using recorded data.
- **Impact:** Enables us to refine this feature for your ease of use.

### **Replay Features**
- **Key Actions Tracked:**
  1. **Candidate Replay:** When you replay a candidate, it's noted.
  2. **Replay Saving:** Saving replays in JSON format is also tracked.
  - **Privacy Note:** We **do not monitor** assertion rules, variable names in these rules, or the assertion JSON.

### **Mock Management**
- **What We Observe:** Injection, activation, or deactivation of mocks.
- **Privacy Assurance:** Details like mock maps or specific lines for mock operations are not tracked.

### **Replay Status Insights**
- **Insight Gathering:** Whether a replay candidate passes or fails.
- **Privacy Commitment:** No tracking of variable names, code blocks, or config files.

### **Privacy Assurance**
- **Offline Functionality:** Operates entirely offline.
- **Non-Intrusive:** No event tracking hinders your workflow.
- **Data Integrity:** Your code and configurations stay private.