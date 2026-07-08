# Ciclo ABM — Alta, Baja y Modificación de usuarios

## Objetivo

Documentar el ciclo de vida completo de una identidad dentro de Microsoft Entra ID, simulando las tres etapas fundamentales de la gestión de accesos que se ejecutan a diario en cualquier entorno corporativo: **Alta** (onboarding), **Modificación** (cambio de rol) y **Baja** (offboarding), incluyendo la asignación de accesos mediante grupos de seguridad (RBAC).

## Escenario simulado

Se simula el ciclo de vida de un colaborador ficticio, **Juan Sánchez**, contratado como Analista de Soporte TI en el área de Operaciones.

## Etapa 1 — Alta (Onboarding)

| Parámetro | Valor |
|---|---|
| **Usuario creado** | Juan Sánchez (jsanchez@willianargumeoutlook.onmicrosoft.com) |
| **Puesto inicial** | Analista de Soporte TI |
| **Departamento** | Operaciones |
| **Ubicación de uso** | Perú |
| **Tipo de usuario** | Miembro |

**Asignación de accesos vía grupo de seguridad:**

| Parámetro | Valor |
|---|---|
| **Grupo creado** | SG-Analistas-Soporte-TI |
| **Tipo de grupo** | Seguridad |
| **Tipo de pertenencia** | Asignada |
| **Miembro agregado** | Juan Sánchez |

En lugar de asignar permisos individuales al usuario, se le agrega como miembro de un grupo de seguridad dedicado. Este es el principio base de RBAC (*Role-Based Access Control*): los accesos y aplicaciones se asocian al grupo, no a la persona, lo que facilita la administración cuando hay rotación de personal o cambios de rol.

## Etapa 2 — Modificación (cambio de rol)

| Parámetro | Antes | Después |
|---|---|---|
| **Puesto** | Analista de Soporte TI | Analista Senior de Soporte TI |

Simula una promoción interna. En un escenario real de producción, este cambio normalmente iría acompañado de una revisión de accesos: el usuario podría necesitar salir de su grupo actual e incorporarse a uno con privilegios adicionales correspondientes a su nuevo rol, evitando así la acumulación de permisos innecesarios (*privilege creep*).

## Etapa 3 — Baja (Offboarding)

| Parámetro | Valor |
|---|---|
| **Acción ejecutada** | Deshabilitar cuenta (Cuenta habilitada = No) |
| **Estado resultante** | Deshabilitado |
| **Cuenta eliminada** | No (se conserva temporalmente) |

## Justificación técnica

- **Deshabilitar antes de eliminar:** al dar de baja a un colaborador, la práctica recomendada es deshabilitar la cuenta de inmediato para bloquear el acceso, mientras se conserva temporalmente el objeto de usuario. Esto permite conservar el historial de auditoría, transferir la propiedad de archivos o buzones si es necesario, y solo eliminar la cuenta de forma definitiva después de un período de retención definido por la política de la organización.

- **Revocación de sesiones (mejora pendiente):** deshabilitar una cuenta bloquea nuevos inicios de sesión, pero no invalida automáticamente tokens de sesión ya emitidos. En un proceso de offboarding real y completo, se recomienda además ejecutar **"Revocar sesiones"** para invalidar de forma inmediata cualquier sesión activa del usuario, cerrando por completo la ventana de acceso.

- **Grupo de seguridad como mecanismo de RBAC:** administrar accesos a través de membresía de grupo, en lugar de asignaciones individuales, reduce el error humano y facilita auditorías masivas — es posible responder "¿quién tiene acceso a X?" revisando la membresía del grupo, en lugar de revisar usuario por usuario.

## Evidencia

*(Capturas de pantalla: perfil de Juan Sánchez con puesto actualizado y cuenta deshabilitada — pendiente de insertar en este documento)*

## Próximos pasos

- Ejecutar "Revocar sesiones" como paso adicional del offboarding y documentar el resultado
- Diseñar la matriz RBAC completa (`02-rbac-matrix`) con roles adicionales y su justificación de diseño
- Evaluar eliminación definitiva de la cuenta tras período de retención simulado
