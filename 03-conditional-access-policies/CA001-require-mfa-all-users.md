# CA001 — Requerir MFA para todos los usuarios

## Objetivo

Implementar una directiva de Acceso Condicional que exija autenticación multifactor (MFA) a todos los usuarios del tenant al acceder a cualquier recurso en la nube, replicando el control base que se implementa en la mayoría de entornos corporativos como primera línea de defensa contra el robo de credenciales.

## Configuración

| Parámetro | Valor |
|---|---|
| **Nombre de la directiva** | CA001 - Require MFA for All Users |
| **Usuarios incluidos** | Todos los usuarios |
| **Usuarios excluidos** | Cuenta de administrador global (buena práctica para evitar bloqueo accidental / *lockout*) |
| **Recursos de destino** | Todos los recursos en la nube |
| **Control de acceso** | Conceder acceso → Requerir autenticación multifactor |
| **Estado de la directiva** | Solo informe (*Report-only*) |

## Justificación técnica

- **Exclusión de la cuenta admin:** en cualquier tenant de producción, aplicar una directiva de MFA a *todos* los usuarios sin excepción —incluyendo la única cuenta de administrador global— crea riesgo de bloqueo total del tenant si el método de autenticación falla. Es una práctica estándar excluir al menos una cuenta de emergencia (*break-glass account*) de las directivas de Conditional Access.

- **Modo "Solo informe":** antes de activar cualquier directiva en producción, se recomienda ejecutarla en modo de solo informe durante un período de observación. Esto permite analizar el impacto real (usuarios afectados, aplicaciones, ubicaciones) en los registros de inicio de sesión antes de aplicar el bloqueo o requisito de forma activa, evitando interrupciones no planificadas al negocio.

## Evidencia

*(Capturas de pantalla de la directiva creada en Microsoft Entra ID — pendiente de insertar en este documento o en carpeta `/screenshots`)*

## Próximos pasos

- Revisar los registros de inicio de sesión en modo "Solo informe" durante un período de prueba
- Evaluar impacto antes de cambiar el estado a "Activado"
- Documentar el siguiente escenario: bloqueo de acceso condicional por ubicación geográfica
