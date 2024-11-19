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
    User entered input is reflected as-is to the webpage without any sanitization. This lends itself to XSS vulnerabilities.
2. Briefly explain how a malicious attacker can exploit them.
    By entering a malicious string (particularly something in a ```<script>``` tag), and hitting submit.
3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
    secure.ts fixes the vulnerability by properly HTML encoding the inputs and sanitizing them before displaying them back to the user.