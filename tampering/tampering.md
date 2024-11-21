# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
Tampering vulnerability is when attackers can change or tamper with the input of an application such that they can achieve unintended behavior. Due to the lack of sanitization of inputs within insecure.ts, the file is vulnerable to attackers inputting many different things like scripts, queries, or even file uploads that are dangerous to our application.

2. Briefly explain how a malicious attacker can exploit them.
A malicious attacker could input a script that takes you to a different site, forces you to download something, or many other nefarious things. Additionally, they could utilize a database query that would expose sensitive data from your database to the public. Lastly, they could upload malicious data to your server through input that could take down or give them control over your application.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
The file secure.ts does not have the same vulnerabilities because it sanitizes the inputs that users send to the server. It utilizes regex patterns to replace different potentially harmful characters with their string equivalents. This means that the inputs from unknown sources will be prevented from performing any unauthorized actions by ensuring the inputs are in string form.