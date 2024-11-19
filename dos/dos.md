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
    There are two possible vulnerabilities. One is that we are using unsanitized user input  in our DB request without a try/catch, which can cause the server to crash due to an unhandled exception. The other is that we have nothing stopping a long running request from stalling the server for an extended period of time.
2. Briefly explain how a malicious attacker can exploit them.
    The first one is simple, by inputting any valid mongoDB query statement ([$ne]=, [$eq], etc.) after id in the URL causes a crash
    The second  one is slightly more difficult in this case because this is a short running  request, but we could send several thousand requests and crash the server by overloading it.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
    The fixes in secure.ts are to add a rate limiter to reduce the potential performance impact on the server from each request, and to wrap the DB request in a try/catch block to prevent a full server crash if something goes wrong.