Cross-Site Scripting (XSS) and Cross-Site Request Forgery (CSRF) are two of the most common web security vulnerabilities. Here's a guide on how to handle these security concerns:

### Cross-Site Scripting (XSS)

XSS attacks occur when an attacker is able to inject malicious scripts into a web page viewed by other users. These scripts can then execute in the users' browsers, leading to unauthorized actions such as stealing cookies, session tokens, or other sensitive information.

#### Best Practices to Prevent XSS:

1. **Input Validation and Sanitization**:
   - Validate and sanitize all user inputs on both client and server sides.
   - Use libraries or frameworks that automatically handle escaping special characters.

2. **Output Encoding**:
   - Encode data before rendering it to the web page to ensure that any HTML special characters are properly escaped.
   - Use functions specific to the context of the data (HTML, JavaScript, CSS).

3. **Content Security Policy (CSP)**:
   - Implement a CSP to restrict the sources from which scripts can be loaded and executed.
   - A CSP can mitigate XSS by disallowing inline scripts and only allowing external scripts from trusted sources.

4. **HTTPOnly Cookies**:
   - Use the HTTPOnly flag on cookies to prevent JavaScript from accessing them.

5. **Secure JavaScript Frameworks**:
   - Utilize modern frameworks like React, Angular, or Vue.js that inherently prevent XSS by escaping data by default.

6. **Avoid Dangerous APIs**:
   - Avoid using `eval()`, `innerHTML`, `document.write()`, and other similar APIs that can execute or inject HTML directly.

### Cross-Site Request Forgery (CSRF)

CSRF attacks occur when a malicious website tricks a user into performing an action on another site where the user is authenticated. This can lead to unauthorized actions being performed on behalf of the user.

#### Best Practices to Prevent CSRF:

1. **Anti-CSRF Tokens**:
   - Implement anti-CSRF tokens (also known as CSRF tokens) for state-changing requests. These tokens should be unique per session and should be included in forms and verified on the server.

2. **SameSite Cookies**:
   - Use the `SameSite` attribute on cookies to prevent them from being sent along with cross-site requests. This restricts cookies to first-party contexts.

3. **Custom Headers**:
   - Require custom headers (like `X-Requested-With: XMLHttpRequest`) for AJAX requests to differentiate between normal browser requests and cross-site requests.

4. **Double Submit Cookie**:
   - Use a double-submit cookie strategy where the CSRF token is sent both as a cookie and as a request parameter. The server checks both values to ensure they match.

5. **Check Referer Header**:
   - Verify the `Referer` header to ensure that the request originated from your own site. However, this can be less reliable as some users or browsers might not send the `Referer` header.

### Implementing Security Practices in Code

#### XSS Example

Here’s how you might handle XSS in a JavaScript context:

```javascript
// Properly encoding user input before displaying it
const encodeHTML = (str) => {
    return str.replace(/&/g, '&amp;')
              .replace(/</g, '&lt;')
              .replace(/>/g, '&gt;')
              .replace(/"/g, '&quot;')
              .replace(/'/g, '&#39;');
}

// Example usage in rendering user input
const userInput = "<script>alert('XSS');</script>";
const safeInput = encodeHTML(userInput);
document.getElementById('output').innerHTML = safeInput;
```

#### CSRF Example

Here’s how you might handle CSRF in a server-side context using Express.js (Node.js framework):

```javascript
// Using csurf middleware in Express.js
const express = require('express');
const csurf = require('csurf');
const cookieParser = require('cookie-parser');

const app = express();
const csrfProtection = csurf({ cookie: true });

app.use(cookieParser());
app.use(express.urlencoded({ extended: true }));

app.get('/form', csrfProtection, (req, res) => {
    res.send(`<form action="/process" method="POST">
                <input type="hidden" name="_csrf" value="${req.csrfToken()}">
                <input type="text" name="data">
                <button type="submit">Submit</button>
              </form>`);
});

app.post('/process', csrfProtection, (req, res) => {
    res.send('Data is being processed');
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

### Summary

By implementing these practices, you can significantly reduce the risk of XSS and CSRF attacks:

- Validate and sanitize all user inputs.
- Encode outputs appropriately.
- Use CSP to restrict the sources for scripts.
- Implement anti-CSRF tokens for state-changing requests.
- Use SameSite cookies to restrict cross-site cookie usage.
- Require custom headers for AJAX requests.
- Verify `Referer` headers when applicable. 

These strategies provide a comprehensive defense against common web vulnerabilities.