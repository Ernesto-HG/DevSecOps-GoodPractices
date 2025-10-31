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

## - Step-by-step setups for projects:

#### 0. Plantilla inicial (archivo README)
#### 1. Repositorio y control de secretos (.gitignore + pre-commit)
   Qué hacer: 
     Ignorar .env y archivos sensibles.
     Añadir hooks que detecten secrets antes del push.
#### 2. Gestión de secretos en producción (no .env en imágenes)
   Qué hacer:
     En producción usa Secret Manager (AWS/ Azure/ GCP/ Vault) o Kubernetes Secrets.
     Nunca COPY .env en Dockerfile; inyecta variables en runtime.
#### 3. Headers de seguridad y hardening HTTP (nginx + Express)
   Qué hacer:
     Añadir CSP, HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Permissions-Policy.
     Usar CSP restrictiva por defecto; permitir sólo lo necesario.
#### 4. Cookies y sesiones
   Qué hacer:
     Marcar cookies sensibles Secure; HttpOnly; SameSite=Lax o Strict.
     Usar sesiones con almacenamiento server-side (redis) y revocación.
#### 5. CORS y SAME-ORIGIN
   Qué hacer:
     Configurar CORS explícitamente en backend, permitiendo orígenes necesarios únicamente.
     Evitar Access-Control-Allow-Origin: * para endpoints con credenciales.
#### 6. Content Security Policy (CSP) — plantilla y proceso
   Qué hacer:
     Crear CSP mínima y poner modo report-to/report-uri para monitorizar.
     Iterar: primero report-only para comprobar rupturas.
#### 7. HSTS y TLS
   Qué hacer:
     Forzar HTTPS, usar TLS 1.2/1.3, configurar suites seguras.
     HSTS con includeSubDomains y preload una vez probado.
#### 8. DNSSEC, OCSP, Certificate Transparency (operacional)
   Qué hacer:
     Activar DNSSEC en el registrador/dns provider.
     Habilitar OCSP stapling en el servidor web.
     Vigilar CT logs / emitir alertas si se emite un certificado nuevo para tu dominio
#### 9. Seguridad de API tokens y secretos
   Qué hacer:
     No almacenar tokens en repos. Usar secret manager y roles IAM.
     Tokens con scopes mínimos y TTL cuando sea posible.
     Implementar revocación y rotación automatizada.
#### 10. CI/CD: control de acceso y automatización de seguridad (Shift-left)
   Qué hacer:
     Proteger branch main con required reviews y MFA en cuentas críticas.
     No permitir merges si hay secret scans o vulnerabilities high.
     Automatizar dependency scanning y SAST/DAST.
#### 11. WAF y rulesets
   Qué hacer:
     Poner WAF delante de la app (Cloudflare, AWS WAF, Azure Front Door) con reglas OWASP CRS básicas.
     Ajustar reglas y excepciones por false positives.
#### 12. Escaneo de vulnerabilidades (DAST/SAST)
   Qué hacer:
     Integrar SAST (static) en PRs y DAST (zap) en pipelines periódicos.
     Hacer pentests anuales y scans después de cambios mayores.
#### 13. Logging seguro y monitoreo
   Qué hacer:
     No loggear secretos o variables completas. Filtrar campos sensibles.
     Estructurar logs (JSON) y centralizar (ELK / Datadog / Grafana Loki).
     Añadir alertas (failed logins anormales, cambios DNS, nuevas certs).
#### 14. Respuesta a incidentes y playbooks
   Qué hacer:
     Tener playbook con pasos: detectar → contener → erradicar → comunicar → lecciones aprendidas.
     Automatizar rotación de claves/secretos como parte de contención.
     
