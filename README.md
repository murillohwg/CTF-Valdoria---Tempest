# Valdoria CTF – Security Writeup

This repository documents the analysis and exploitation process of a CTF-style technical challenge focused on web application security.

The objective was to investigate the target application, identify vulnerabilities, and obtain access to restricted administrative resources.

---
# Skills Demonstrated

• Web Application Security Testing  
• JWT Authentication Analysis  
• OSINT Investigation  
• HTTP Request Manipulation  
• Custom Python Automation  

---
# Tools Used

- Burp Suite
- Python
- curl
- Browser DevTools

---
# Vulnerabilities Identified

### 1. Confidential File Discovery

During the investigation phase, several confidential files were discovered containing hashed identifiers by exploring some ocult directories and then using a script in python to decode the hash.


A custom Python script was developed to brute-force potential date values and match them against the observed hash.

Script available in:

´´Scripts/decrypt.py´´

---
### 2. JWT Authentication Bypass

The application used JSON Web Tokens (JWT) for authentication.

However, the backend failed to properly validate the token signature.

By modifying the token header algorithm to **"none"**, it was possible to craft a token with administrative privileges.

Example structure:

Header
{
"alg": "none",
"typ": "JWT"
}

Payload
{
"name": "Tavares Lunik Bernardi",
"role": "operador"
"Authorization": "Beare TOKEN_JWT_FORMAT"
}

This allowed unauthorized access to internal data exposed by the administrative dashboard.

---
# Evidence

Screenshots demonstrating the exploitation process are available in the **screenshots/** directory.

Examples include:

- JWT token manipulation
- Admin dashboard access
- Intercepted HTTP requests

---
# Lessons Learned

This challenge reinforced several important security concepts:

- Improper JWT validation can completely break authentication systems
- Confidential files may expose hidden attack surfaces
- Automation with Python can significantly speed up investigation processes

---
# Disclaimer

This repository documents a CTF-style security challenge performed in a controlled and authorized environment for educational purposes.
