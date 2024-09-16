# Stored vs Reflected XSS Theory
**Introduction to Web Application Attacks**  
**December 29, 2023**

### XSS Overview:
- **Stored (Persistent) XSS**: The exploit or payload is stored in the database of the web server or cached by the server. This type of attack targets multiple users, as the payload is served to anyone who accesses the affected resource.
- **Reflected XSS**: The payload is part of a crafted request or link and is immediately reflected back to the user. It primarily attacks the person who submits the request.
- Both stored and reflected XSS can be used on the client side (browser) or server-side.

### DOM-based XSS:
- The browser parses the page's HTML content and generates an internal DOM representation.
- DOM-based XSS occurs when a page's DOM is modified using user-controlled values.
- This type of XSS can be either stored or reflected, depending on how the payload is delivered.

---

# XSS Payload Execution Context
**Introduction to Web Application Attacks**  
**December 29, 2023**

No matter how the XSS payload is delivered (stored, reflected, or DOM-based), the injected scripts run in the context of the user visiting the affected page. This means that the user's browser—not the web application—executes the XSS payload.

---

# JavaScript Refresher
**Introduction to Web Application Attacks**  
**December 29, 2023**

Modern web applications run on JavaScript (JS) engines. When a browser processes an HTTP response containing HTML, it creates a DOM tree and renders it, representing every component of the page (e.g., inputs, images, etc.).  
- JS allows access to and manipulation of the DOM, enhancing user interactivity.  
- If we inject code into JS, we can modify the DOM, redirect logins, extract passwords, and steal session cookies.

---

# Identifying XSS Vulnerabilities
**Introduction to Web Application Attacks**  
**December 29, 2023**

### How to Identify XSS Vulnerabilities:
- Look for injection points where characters such as `<`, `>`, `'`, `"`, `{}`, and `;` are used.
  - **HTML Elements**: `<`, `>`
  - **JS Functions**: `{}`
  - **Strings**: `'`, `"`
  - **Semicolons**: `;`

### Encoding Types:
- **HTML Encoding**: For instance, using `&lt;&gt;` allows characters like `<` and `>` to be shown as plain text rather than interpreted as HTML tags.

---

# Privilege Escalation via XSS
**Introduction to Web Application Attacks**  
**January 02, 2024**

### Privilege Escalation Using XSS:
- HTTP-only encrypted connections prevent JavaScript from accessing cookies.
- Use the **Storage tab** in browser DevTools to view cookie settings.
- **Attack Example**: A JavaScript payload is loaded into the user agent field via a visitor plugin, allowing a command to create an admin account.
  - Example: A JS script to create an admin account in WordPress.

### NONCE:
A nonce is a web token generated to prevent **Cross-Site Request Forgery (CSRF)**, which is a social engineering attack where the victim clicks on a malicious link that triggers an action.

---

# Inspecting HTTP Response Headers and Sitemaps
**Introduction to Web Application Attacks**  
**May 15, 2024**

### Web Application Enumeration:
- The file extension of pages can reveal the programming language used to develop the application (e.g., `.php` for PHP).
- Routes allow developers to map a URL to specific sections of code.

### Inspecting HTTP Responses:
1. Use a proxy or browser's network tools to analyze responses.
2. Check for headers under **Network > Headers** to view server versions.
3. Headers starting with `X-` are deprecated and non-standard.

### Sitemaps:
- `/robots.txt` helps crawlers correctly index a site.

---

# Enumerating and Abusing APIs
**Introduction to Web Application Attacks**  
**May 15, 2024**

### API Enumeration and Abuse:
- **API**: Application Programming Interface.
- Use tools like `gobuster` to enumerate API directories and identify potential vulnerabilities for exploitation.
