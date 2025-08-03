# Dependency Confusion

### What is Dependency Confusion?

**Dependency Confusion** (a.k.a. **Substitution Attack**) occurs when an application **inadvertently installs a malicious public package** instead of the intended **private/internal one**, due to a name collision and the way package managers resolve dependencies.

This attack exploits the **trust assumptions** developers make between public and private package repositories.

---

### How It Works

1. An application uses a package called `internal-logger` from a **private registry**.
2. An attacker identifies this internal package name (e.g., from leaked files or metadata).
3. The attacker publishes a **public package** with the **same name** (`internal-logger`) and a **higher version number**.
4. The package manager (like npm, pip, or yarn) **prefers the public one**, thinking it's a newer version.
5. Boom! Malicious code gets installed in the target environment.

---

### Real-World Example

| Component             | Value                                |
| --------------------- | ------------------------------------ |
| 🔒 Private Package    | `internal-logger`                    |
| 🎭 Attacker Publishes | `internal-logger` on public registry |
| 📈 Higher Version     | `1.0.1` (vs internal `1.0.0`)        |
| 💥 Outcome            | Public malicious package is pulled   |

---

### How to Identify Potential for Exploitation

1. **Enumerate Internal Package Names**

   * Look into:

     * `package.json` (npm)
     * `requirements.txt` (pip)
     * `.csproj` / `packages.config` (.NET)
     * Build logs or error messages
     * `.lock` files

2. **Publish a Public Package**

   * Use the same name as the internal package
   * Give it a higher version number

3. **Monitor Callbacks**

   * Set up DNS or HTTP beacons in the package
   * Watch for telemetry from the victim (e.g., CI/CD pipeline)

---

### Mitigation Techniques

* Configure your package manager to **prioritize internal/private registries**.
* Use **scoping** for internal packages (`@your-org/package-name` in npm).
* Implement **allow lists** for trusted registries.
* Regularly audit your dependency resolution process.

---

### 📚 References

* 🔗 [HackerOne Report by Alex Birsan](https://hackerone.com/reports/946409)
* 🔗 [x1337loser GitHub - Dependency Confusion](https://github.com/x1337loser/Dependency-Confusion)
