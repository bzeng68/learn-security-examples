# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
Repudiation vulnerability means that an attacker is able to access resources or perform actions on the system without being traced or tracked. This can take form in lack of logging or auditing, or in tampered logs. Insecure.ts lacks logging or any form of operation tracking, there is no way for the system to identify what a user has done. Additionally, there is no data persistence in the logging, so the logging disappears once the server has been shut off.

2. Briefly explain why the vulnerability is addressed in __secure.ts__.
The vulnerability is addressed in secure.ts by adding middleware into the application that logs information about incoming responses and errors that occurred in the system. This middleware's logs are persisted by writing the logs to a file on the server's local system. This logging and data persistence of logs enables tracking and tracing of every access that happens with the server. This style of logging also facilitates automated auditing of logs as you can determine the format of the logs and create scripts accordingly.

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
The chain of responsibility design pattern is being used in the secure version to address the repudiation vulnerability by adding additional request and error logging to the application. The middleware handles a request and logs its information, then passes the request through to the endpoint handler where the request is handled. If the operation errors at any point, the request is sent to the error handler middleware that logs the error and then it is finally sent back to the user as an error response. This is the chain of responsibility design pattern because the request gets passed through a series of handlers that either process the request or pass it off to the next handler.