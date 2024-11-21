# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.
Spoofing vulnerability is when attackers are able to identify as other people using their data in order
to gain unauthorized access. Due to lack of HttpOnly and SameSite attributes for the cookies used in 
sessions in insecure.ts, the file is vulnerable to these types of attacks as attributes for the cookies provided by the session are not restrictive enough.

2. Briefly explain different ways in which vulnerability can be exploited.
This spoofing vulnerability can be exploited by either session hijacking or CSRF. Session hijacking refers to obtaining the cookies for a session and using the cookies to identify as a user to perform unauthorized requests. This can be done in insecure.ts by creating a link that has JavaScript in it, which runs and logs the cookie data of the user once they have clicked on the link. Meanwhile, CSRF refers to cross-site request forgery, which can be done in insecure.ts by creating a form that is automatically submitted once a user loads the site. This form sends a request to the server as the user who loaded the malicious site, allowing them to use their cookie in the request.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
Secure.ts does not have the spoofing vulnerability in insecure.ts because it uses the HttpOnly
and SameSite attributes of session cookies such that it prevents access of cookies from anything besides
HTTP requests/responses and prevents cookies from being used in requests that do not originate from
the site that had provided the cookies initially.