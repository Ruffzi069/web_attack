```markdown
# ☕ Spring Boot Actuator Misconfiguration

Spring Boot Actuator is like a **built-in dashboard** for your Spring Boot applications. It provides production-ready features to help monitor and manage your app via HTTP endpoints.

---

## 🚀 What is Spring Boot Actuator?

Actuator provides endpoints to check:

- Application **health**
- **Configuration** settings
- **Performance** metrics
- And more...

### 🔍 Common Endpoints:
- `/actuator`
- `/actuator/health`
- `/actuator/env`
- `/actuator/heapdump`

---

## ⚠️ Misconfiguration Risk

If **actuator endpoints are not secured**, they may expose **sensitive data**:

- App configuration and secrets (`/env`)
- JVM memory dumps (`/heapdump`)
- Runtime environment variables
- Service status

> 🧨 This can lead to **information disclosure**, **recon**, or **post-exploitation** opportunities.

---

## 🔎 How to Find Actuator Exposed Endpoints

### 🕵️ Search Engine Dorking

**FOFA:**
```

body="Whitelabel Error Page"

```

**Shodan:**
```

http.favicon.hash:"116323821"

```

---

### 🧪 Manual Scanning

Try accessing:
```

[http://target:8080/actuator](http://target:8080/actuator)
[http://target:8080/actuator/env](http://target:8080/actuator/env)
[http://target:8080/actuator/heapdump](http://target:8080/actuator/heapdump)

```

These can be tested directly in the browser or with tools like curl.

---

## 📚 References

- 🔗 [HackerOne Report #304386](https://hackerone.com/reports/304386)
- 🔗 [Wiz Blog: Spring Boot Actuator Misconfigurations](https://www.wiz.io/blog/spring-boot-actuator-misconfigurations)

---

> 🧠 Always ensure authentication is enforced on sensitive actuator endpoints.
```
