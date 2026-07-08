# IAM & Access Governance Lab

Laboratorio práctico de gestión de identidades y accesos (IAM) construido sobre Microsoft Entra ID, documentando escenarios reales de gobierno de identidades que replican los controles administrados en producción para +200 usuarios en un entorno multinacional (GesNext / IBM).

## 📁 Contenido del repositorio

### [01 — Ciclo ABM](./01-abm-cycle)
Ciclo de vida completo de una identidad: Alta con asignación de accesos vía grupo de seguridad (RBAC), Modificación de rol, y Baja (offboarding) con deshabilitación de cuenta.

### [03 — Políticas de Acceso Condicional](./03-conditional-access-policies)
- **CA001:** Requerir MFA para todos los usuarios
- **CA002:** Bloqueo de acceso fuera de Perú

## 🧩 Stack técnico

- Microsoft Entra ID (Azure AD) + Entra ID P2 (Conditional Access)
- Grupos de seguridad y RBAC
- Microsoft 365 Developer Tenant (entorno de laboratorio)

## 🎯 Contexto

Este laboratorio se desarrolla en paralelo a mi preparación para la certificación **SC-300: Microsoft Identity and Access Administrator**, formalizando de manera pública competencias que aplico diariamente en mi rol profesional como Líder de Operaciones TI y Seguridad.

## 📫 Contacto

[LinkedIn](https://linkedin.com/in/willianargume) · willian.argume@gmail.com
