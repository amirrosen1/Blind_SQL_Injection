# 🕵️ Blind SQL Injection – Exercise 4

This repository contains the solution for **Exercise 4 – Blind SQL Injection**  
from the Cybersecurity Lab (67607) at the Hebrew University.

---

## 📚 Overview

This project demonstrates a **Blind SQL Injection** attack where the web application does **not display** database results directly.  
Instead, the attacker deduces information by sending specially crafted payloads and analyzing **boolean-based HTTP responses**.

---

## 🔍 Attack Summary

- Extracts the **password** of a user with ID `336224076`.
- Sends bitwise SQL injection payloads via HTTP GET requests.
- Reconstructs each character bit-by-bit from the server's behavior.
- Stops extraction on null character (`\0`) or after max queries (`100`).

**Injected SQL payload:**

```sql
/index.php?order_id=4 UNION SELECT ((ASCII(SUBSTRING(password, %d, 1)) >> %d) & 1) FROM users WHERE id='336224076'--
