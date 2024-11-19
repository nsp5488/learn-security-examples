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
    There is a privilege escalation vulnerability since there is no real authentication or authorization before modifying sensitive information.
2. Briefly explain how a malicious attacker can exploit them.
    The attacker can just guess user IDs until they find the admin's ID and then execute the form as the admin.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
    secure.ts implements session-based authentication and then uses that to verify that the user has logged in.