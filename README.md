# DevSecOps-GoodPractices
Good practice settings for new web development projects
## Contents:
- SOC (Same-Origin policy) & CORS (Cross-Origin Policy)
- Cookies (SameSiteLax & SameSiteStrict)
- .env
- CSP
- X-frame & X-Content-Type-Options
- Referrer & Permission policies
- HSTS
- Header security
- DNSSEC, OCSP, Certificate Transparency.
- Seguridad de API tokens y secretos (no subir .env ni claves a repositorios).
- Hardening de infraestructura
- WAF (Web Application Firewall)
- Escaneo de vulnerabilidades (OWASP ZAP, Burp Suite)
- Control de acceso en CI/CD y servidores.
- DevSecOps y Shift Left Security
- Automatizar auditorías de seguridad en el pipeline (Snyk, Dependabot, GitHub Actions).
- Logging seguro y monitoreo

## - Step-by-step setups for projects (Shift left security):

0. Initial commit (README)
1. Repositories and secret control (.gitignore + pre-commit)
2. Production secret management (no .env in images)
3. Security headers and HTTP hardening (nginx + Express)
4. Cookies and sessions
5. CORS and SAME-ORIGIN
6. Content Security Policy (CSP) — template and process
7. HSTS and TLS
8. DNSSEC, OCSP, Certificate Transparency (operational)
9. API security: tokens and secrets
10. CI/CD: access control and security automation (Shift-left)
11. WAFs and rulesets
12. Vulnerability scanning (DAST/SAST)
13. Secure logging and monitoring
14. Incident response and playbooks

## XSS, CSRF & Dom XSS utility table

| Renderizado | Ataque principal | Vector | Cabeceras clave | Solución base |
|--------------|------------------|---------|------------------|----------------|
| SSR | XSS / CSRF | ViewBag, Model | CSP, HSTS, X-Frame-Options | escape & validate inputs; Anti-CSRF |
| CSR | DOM XSS / iframe abuse | innerHTML, postMessage | CSP, X-Frame-Options, Permissions-Policy | Avoid raw HTML; sanitize DOM |
| Híbrido | Combinado | SSR + DOM | CSP, HSTS, Referrer-Policy | Sanitize both sides; report-only CSP |

## Software architecture related:

| Área                                       | Risks                                           | Good practices                                         |
| ------------------------------------------ | --------------------------------------------------------------- | --------------------------------------------------------------------- |
| **Layered (n-tier, clean, onion)** | Responsabilities fusion, data exposure, SQL injection | domain seggregation, infraestructure & presentation, SOLID principles |
| **Identity & access management (IAM)** | Privilege scaling, token leak                         |  OAuth2, OpenID Connect, safe JWT                    |
| **Communication**                         | Data interception, MITM                                   | HTTPS/TLS, on-transport encryption                           |
| **Persistence & storage**          | Data filtering, corruption                                 | idle encryption, ORM with validations and sanitization                  |
| **Microservices / APIs**                  | Deserialization attacks, Exposed APIs                      | Safe gateways, API Keys, rate limiting, centralized validation      |
| **Events / Messaging**                   | Reproduction or message injection                            | Safe queues, message signatures (RabbitMQ con TLS, etc.)               |
| **Deployment & DevOps**                    | Exposed credentials, CI/CD issues                        | Secret management, zero-trust, container scanning                |


