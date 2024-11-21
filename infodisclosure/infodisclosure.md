# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
Information disclosure vulnerability means that attackers are able to obtain personal or system sensitive information without authorization. Insecure.ts directly references an unverified and unsanitized request within a query to the database collection User that contains sensitive login information in the form of usernames and passwords.

2. Briefly explain how a malicious attacker can exploit them.
A malicious attacker could exploit this vulnerability by performing a SQL or noSQL injection on the application. These injections are when attackers input database commands into their request instead of an real and allowed input. This allows them to be able to access database documents and subsequently use that information nefariously. For example, an attacker could use this to access someone's login information and then log into their account to purchase things using their saved payment methods.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
Secure.ts prevents information disclosure by sanitizing the input from the request. It first type checks that the input is a string and follows that up by using regex to remove any non-alphanumeric values from the string. This means that input from the user is known to be an allowed string before it is used to access the database, protecting the database from unauthorized disclosure or leakage.