Here’s a formatted version of the explanation for your **GitHub README**:

---

# Monitoring AWS Console Sign-Ins Using CloudTrail and EventBridge

This architecture demonstrates how to monitor **AWS Management Console sign-ins** and send alerts using AWS services like CloudTrail, EventBridge, and SNS. Below is a detailed explanation of the setup:

---

## **Architecture Overview**

### **Components**
1. **AWS IAM**:
   - **Root User and IAM Users**:
     - Represents the entities attempting to sign in to the AWS Management Console.
     - Sign-in activities are logged by **CloudTrail**.

2. **AWS CloudTrail**:
   - Tracks **console sign-in events** (e.g., successful and unsuccessful login attempts for root and IAM users).
   - Captures detailed event information:
     - User identity.
     - Timestamp of the activity.
     - Source IP address.

3. **Amazon EventBridge**:
   - Event router that listens for specific patterns of events logged by **CloudTrail**.
   - Filters **console sign-in events**, particularly for sensitive accounts like the **root user**.
   - Triggers actions, such as sending alerts.

4. **Amazon SNS (Simple Notification Service)**:
   - **SNS Topic**:
     - Sends alerts to subscribers via email, SMS, or other channels.
     - In this setup, EventBridge sends sign-in alerts to an SNS topic named `ConsoleAlerts`.

5. **Security Operations**:
   - Represents the team or entity receiving the notifications.
   - Subscribers to the SNS topic are alerted of any suspicious activity and can take appropriate action.

---

## **How the Process Works**

1. **Sign-In Activity**:
   - A user (either the **root user** or an **IAM user**) attempts to sign in to the AWS Management Console.

2. **Event Logging**:
   - CloudTrail logs the **ConsoleSignIn** event in near real-time.
   - Event details include the username, source IP address, and the outcome of the login attempt (success or failure).

3. **EventBridge Filtering**:
   - EventBridge is configured with a **rule** to match specific patterns in CloudTrail logs, such as:
     - Root account sign-ins.
     - Sign-ins from unusual IP addresses.
   - Matching events are sent to an SNS topic.

4. **Alert Delivery**:
   - SNS sends alerts to all subscribers of the topic (e.g., via email or SMS).
   - Example topic: `ConsoleAlerts`.

5. **Security Monitoring**:
   - The **Security Operations** team reviews the alerts and determines if the activity is authorized.
   - Unusual or unauthorized activity can trigger incident response actions.

---

## **Purpose of the Architecture**

- **Real-Time Monitoring**: Tracks critical console sign-ins as they happen.
- **Enhanced Security**: Monitors root user sign-ins (a high-risk activity).
- **Automated Alerts**: Reduces manual effort by notifying the security team immediately.
- **Compliance**: Helps meet audit and compliance requirements by monitoring sensitive AWS activities.

---

## **Example Use Case**
Imagine a scenario where the **root account** is accessed unexpectedly:
1. The system sends an alert to the **Security Operations** team.
2. The team verifies if the login was legitimate.
3. If unauthorized, the team can take immediate action, such as:
   - Restricting access.
   - Rotating credentials.
   - Investigating further for potential breaches.

---

### **Architecture Diagram**

*Include the image or diagram here.*

---

Feel free to let me know if you'd like further edits or additional sections!
