# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
Privilege escalation vulnerability means that attackers are able to grant themselves unauthorized privileges that enable to perform unpermitted actions like accessing resources that they normally should not be able to. Insecure.ts gets the user id and role directly from the request body without any sanitization or anything. This means that authentication gets determined by the user and not the server, allowing attackers to potentially authenticate themselves with privilege higher than they should have.

2. Briefly explain how a malicious attacker can exploit them.
A malicious attacker can try out different inputs to find an account or some method to authenticate themselves with a higher privilege than they should have. This means that they will be able to access resources, actions, and operations from the application that they should not be able to. 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
In secure.ts, we establish a session with httpOnly and sameSite attributes to ensure that authentication is handled by our own application and is secured through the use of cookies with attributes to protect against CSRF and other spoofing. Additionally, the endpoint references the session attribute of the request which we trust because our application had given the user a specific cookie that was hashed with our secret attached to it.