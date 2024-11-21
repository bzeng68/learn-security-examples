# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
A denial of service vulnerability means that attackers are able to overwhelm a service with requests or exploit a vulnerability to prevent it from servicing requests. Insecure.ts does not handle errors that might occur in a database query or any other action, sanitize inputs to authorized strings, or rate limit the amount of requests that an IP can send to the server.

2. Briefly explain how a malicious attacker can exploit them.
A malicious attacker can try out different inputs in order to try and crash the server by causing either a database operation or system operation to throw an uncaught error. Additionally, they could continuously send requests to the server to either hog all the bandwidth of the service such that other users cannot utilize the service or crash the service all together.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
Secure.ts encases the endpoint logic in a try catch block that ensures that any errors thrown are caught and handled accordingly such that the server does not go down when an error is thrown. Additionally, it adds a piece of middleware to rate limit the number of requests that an IP can send within a certain timeframe to the service such that the service will never be overwhelmed. Although it doesn't do this currently, secure.ts should also sanitize input so that errors will not occur in the first place.