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
    The insecure code has no logging, so any incoming requests could be from any user without the server being able to see what those requests were.
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
    In secure.ts, all incoming requests are properly logged by the middleware.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
    Chain of responsibility is used here, with the logging middleware handling the logging of each request before passing the request to the next handler.