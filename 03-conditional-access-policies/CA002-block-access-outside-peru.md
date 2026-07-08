# CA002 — Bloqueo de acceso fuera de Perú

## Objetivo

Implementar una directiva de Acceso Condicional que bloquee el acceso a los recursos del tenant desde cualquier ubicación fuera de Perú, restringiendo el inicio de sesión a la ubicación geográfica esperada de la organización. Este control reduce la superficie de ataque frente a intentos de acceso no autorizado desde el extranjero, incluso si las credenciales de un usuario fueran comprometidas.

## Configuración

| Parámetro | Valor |
|---|---|
| **Nombre de la directiva** | CA002 - Block Access Outside Peru |
| **Usuarios incluidos** | Todos los usuarios |
| **Usuarios excluidos** | Cuenta de administrador global (evita bloqueo accidental / *lockout*) |
| **Recursos de destino** | Todos los recursos en la nube |
| **Ubicación con nombre creada** | "Perú" (determinación por dirección IP, IPv4 e IPv6) |
| **Condición de ubicación** | Excluir: Perú (la directiva aplica a todo acceso, excepto el que proviene de Perú) |
| **Control de acceso** | Bloquear acceso |
| **Estado de la directiva** | Solo informe (*Report-only*) |

## Justificación técnica

- **Uso de "Ubicaciones con nombre":** antes de crear la directiva, fue necesario definir una ubicación con nombre para Perú en Acceso Condicional. Esto permite reutilizar la misma definición geográfica en múltiples directivas futuras sin reconfigurar rangos de IP o países cada vez.

- **Lógica de inclusión/exclusión invertida:** a diferencia de CA001 (que incluye a todos y excluye al admin), aquí la condición de ubicación funciona en sentido inverso: se aplica el bloqueo a *cualquier ubicación excepto Perú*. Esto es más seguro que intentar enumerar manualmente "todos los países no autorizados", ya que cualquier país nuevo queda bloqueado por defecto.

- **Modo "Solo informe":** al igual que en CA001, esta directiva se mantiene en modo de solo informe para analizar el impacto real antes de activarla — es especialmente importante aquí porque un bloqueo geográfico mal configurado podría afectar a usuarios legítimos en viaje, VPNs corporativas con salida internacional, o servicios en la nube con IPs fuera del país.

## Evidencia

*(Captura de pantalla de las 2 directivas activas en el tenant — pendiente de insertar en este documento)*

## Próximos pasos

- Revisar registros de inicio de sesión en modo "Solo informe" para validar que no haya falsos positivos (ej. accesos legítimos bloqueados por error)
- Evaluar activación conjunta con CA001 (MFA + restricción geográfica combinadas)
- Documentar el ciclo ABM (Alta, Baja, Modificación) de usuarios como siguiente entregable del repositorio
