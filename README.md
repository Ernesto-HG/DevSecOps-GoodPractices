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

#### 0. Plantilla inicial (archivo README)
#### 1. Repositorio y control de secretos (.gitignore + pre-commit)
#### 2. Gestión de secretos en producción (no .env en imágenes)
#### 3. Headers de seguridad y hardening HTTP (nginx + Express)
#### 4. Cookies y sesiones
#### 5. CORS y SAME-ORIGIN
#### 6. Content Security Policy (CSP) — plantilla y proceso
#### 7. HSTS y TLS
#### 8. DNSSEC, OCSP, Certificate Transparency (operacional)
#### 9. Seguridad de API tokens y secretos
#### 10. CI/CD: control de acceso y automatización de seguridad (Shift-left)
#### 11. WAF y rulesets
#### 12. Escaneo de vulnerabilidades (DAST/SAST)
#### 13. Logging seguro y monitoreo
#### 14. Respuesta a incidentes y playbooks

## XSS, CSRF & Dom XSS utility table

| Renderizado | Ataque principal | Vector | Cabeceras clave | Solución base |
|--------------|------------------|---------|------------------|----------------|
| SSR | XSS / CSRF | ViewBag, Model | CSP, HSTS, X-Frame-Options | Escapar y validar entradas; Anti-CSRF |
| CSR | DOM XSS / iframe abuse | innerHTML, postMessage | CSP, X-Frame-Options, Permissions-Policy | Evitar HTML directo; sanitizar DOM |
| Híbrido | Combinado | SSR + DOM | CSP, HSTS, Referrer-Policy | Sanitizar en ambos lados; report-only CSP |

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


