# HTML Injection

### Severity:

Typically **P3 or P4**, as HTML Injection is a **client-side vulnerability**. However, its impact can escalate if chained with other bugs (e.g., XSS or phishing vectors).

---

### What is HTML Injection?

HTML Injection occurs when **untrusted user input** is inserted directly into a webpage’s HTML structure **without proper sanitization**. This allows attackers to inject arbitrary HTML elements, potentially affecting the page's appearance or behavior.

---

### Common Attack Surface

This vulnerability often arises when:

* The application reflects unsanitized input back into the response.
* No server-side validation or encoding is enforced.
* Client-side controls (like HTML editors) are blindly trusted.

---

### Example Vectors

**Injectable HTML Tags** (commonly used):

```html
<h1>, <h2>, <h3>, <br>, <img>, <b>, <i>
```

---

### Types of HTML Injection

#### 1. **GET-Based Injection**

* Occurs via query parameters in the URL.
* Example:

  ```url
  https://example.com/search?query=<h1>Injected</h1>
  ```
* Common in:

  * Search bars
  * Profile views
  * URL-based form pre-fillers

#### 2. **POST-Based Injection**

* Occurs when data is submitted via a form.
* Example targets:

  * Contact forms
  * Comment sections
  * Login/signup fields

---

### Bug Bounty Potential

HTML Injection is frequently classified as **informational to low severity**, but:

* You can **easily earn \$50–100** per report on platforms like HackerOne or Bugcrowd.
* Impact increases if it leads to:

  * **UI redress (phishing)**
  * **Content spoofing**
  * **Client-side script injection prep**

---

### Where to Look

Look for unsanitized user input reflected in:

* Profile names / bios
* Feedback forms
* Custom UI messages
* Error responses
* Search queries

---

### Reference

* [HTML Injection Simple $500](https://hackerone.com/reports/1581499)
* [HTML Injection MyCrypto](https://hackerone.com/reports/324548)
