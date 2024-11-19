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
    Because the cookies are able to be used from any site (sameSite is off), if a cookie is intercepted by a man in the middle it can be used to access privileged information via a spoofing attack.
    Since the cookies are also not httpOnly, scripts can extract the cookie and use its token for future requests, thus enabling a different form of the spoofing attack
2. Briefly explain different ways in which vulnerability can be exploited.
    One of the ways to exploit the vulnerability is through cross-site request forgery, by submitting a request to the vulnerable server, since sameSite is disabled on the cookie, the browser will automatically pass the cookie to the vulnerable website and allow for requests to be made.
    Another way to exploit the vulnerability is by using a script to capture the vulnerable cookies so that they can be used for future attacks.
3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
    secure.ts fixes the vulnerabilities by enabling sameSite and httpOnly on the cookies.