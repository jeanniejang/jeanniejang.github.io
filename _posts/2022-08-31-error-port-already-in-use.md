---
title: "Port already in use error"
categories: Error
tag: [Java, Spring, errors]
toc: true
---

🆘 How I solved the errors that I encountered
{: .notice--danger}

## Error message
```
Description:

Web server failed to start. Port 8080 was already in use.

Action:

Identify and stop the process that's listening on port 8080 or configure this application to listen on another port.
```
## Solution
The error message and the solution for this issue is very straight forward.  
In my case, I was already using port 8080 for another program, so I changed the port number to 8081 by announcing it in the application.properties file.
The number of the port can be changed.

### Full code
```java
server.port=8081
```