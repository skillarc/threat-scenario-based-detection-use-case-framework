# 4. Fases del escenario y automatización temprana

> **Threat Scenario-Based Detection Use Case Framework — Draft v0.2**

## 4.1 Objetivo

Uno de los objetivos principales de la v0.2 es reducir el tiempo entre **detección** y **contención**, especialmente durante las primeras fases del escenario.

La hipótesis operativa es:

> Cuanto antes pueda confirmarse un comportamiento adversario con suficiente confianza, menor será el costo y el impacto potencial de la respuesta.

Por ello, el framework busca que determinadas UD de **Reconocimiento** y **Acceso inicial** puedan activar acciones automáticas o semiautomáticas antes de que el adversario alcance Ejecución, Persistencia, Movimiento lateral o Impacto.

## 4.2 Fases

### Fase 1 — Reconocimiento

Busca identificar actividad destinada a conocer superficie, servicios, usuarios, tecnologías o condiciones explotables.

Ejemplos de comportamientos:

- escaneo de puertos;
- enumeración de servicios;
- acceso repetitivo a rutas sensibles;
- reconocimiento de aplicaciones;
- búsqueda de usuarios válidos;
- sondeo de VPN, WAF o portales publicados.

### Fase 2 — Acceso inicial

Busca identificar intentos o eventos que puedan otorgar acceso a un activo o servicio.

Ejemplos:

- password spraying;
- fuerza bruta;
- autenticación anómala;
- explotación de servicio expuesto;
- uso de credenciales comprometidas;
- acceso desde infraestructura adversaria.

### Fase 3 — Ejecución / Acción

Incluye la ejecución de comandos, herramientas, scripts, binarios o acciones relevantes posteriores al acceso.

### Fase 4 — Persistencia / Movimiento lateral

Incluye mecanismos destinados a mantener acceso o ampliar alcance dentro del entorno.

### Fase 5 — Exfiltración / Impacto

Incluye extracción de información, cifrado, destrucción, indisponibilidad, fraude u otro efecto final.

## 4.3 Principio de automatización por UD

La automatización debe asociarse a la **UD**, no únicamente al escenario.

Cada UD debe declarar:

- nivel de confianza;
- criticidad;
- entidad afectada;
- acción candidata;
- impacto potencial de la acción;
- reversibilidad;
- condiciones adicionales requeridas;
- tiempo máximo de respuesta;
- nivel de automatización autorizado.

## 4.4 Niveles de automatización

| Nivel | Tipo | Ejemplo |
|---|---|---|
| 0 | Observación | Generar señal y evidencia |
| 1 | Enriquecimiento | Reputación, geolocalización, identidad, activo |
| 2 | Recomendación | Proponer bloqueo o suspensión para aprobación |
| 3 | Contención reversible | Bloqueo temporal de IP, cierre de sesión, aislamiento temporal |
| 4 | Respuesta de alto impacto | Deshabilitación de servicio o cuenta crítica bajo gobernanza estricta |

## 4.5 Automatización en Reconocimiento

Las UD de Reconocimiento son candidatas principalmente a automatización de bajo impacto y reversible.

### Patrón A — Escaneo de puertos

**UD:** múltiples conexiones a puertos diferentes desde un mismo origen dentro de una ventana temporal.

Posibles acciones:

1. enriquecer reputación, ASN y geolocalización;
2. validar si el origen pertenece a una lista autorizada;
3. elevar puntuación de riesgo;
4. correlacionar con otras UD del mismo origen;
5. aplicar bloqueo temporal si se cumplen criterios adicionales.

### Patrón B — Enumeración repetitiva de servicios

**UD:** acceso secuencial o masivo a múltiples rutas, servicios o recursos publicados.

Posibles acciones:

- activar rate limiting;
- incrementar nivel de inspección;
- agregar origen a watchlist;
- bloquear temporalmente cuando exista alta confianza;
- iniciar correlación con intentos posteriores de autenticación.

## 4.6 Automatización en Acceso inicial

Esta fase ofrece el mayor valor para una contención temprana basada en UD correlacionadas.

### Patrón A — Password Spray

**UD:** un mismo origen intenta autenticarse contra múltiples usuarios en una ventana corta.

Cadena de respuesta sugerida:

**Detectar**  
→ **Enriquecer origen**  
→ **Validar exclusiones**  
→ **Correlacionar con reputación / geolocalización / histórico**  
→ **Bloqueo temporal del origen**  
→ **Notificación**  
→ **Seguimiento de usuarios atacados**

### Patrón B — Fuerza bruta sobre una cuenta

**UD:** múltiples fallos de autenticación contra un mismo usuario.

Acciones candidatas:

- enriquecimiento del origen;
- correlación con actividad previa;
- rate limiting;
- bloqueo temporal de origen;
- solicitud de MFA adicional;
- seguimiento de autenticación satisfactoria posterior.

### Patrón C — Éxito posterior a múltiples fallos

**UD:** autenticación satisfactoria precedida por una secuencia de intentos fallidos relacionados.

Esta UD debe considerarse de mayor prioridad porque modifica el contexto desde intento hacia posible acceso.

Acciones candidatas:

- cerrar sesión activa;
- revocar o renovar tokens;
- forzar cambio de credenciales;
- incrementar nivel de autenticación;
- bloquear temporalmente el origen;
- iniciar investigación prioritaria.

La ejecución automática de estas acciones debe depender del contexto de identidad, criticidad de la cuenta y confianza de la correlación.

## 4.7 Correlación entre UD

El valor aumenta cuando varias UD se correlacionan.

Ejemplo:

**UD-R01:** escaneo de puertos  
+  
**UD-R02:** enumeración de portal VPN  
+  
**UD-A01:** password spray  
+  
**UD-A02:** autenticación satisfactoria posterior a fallos

La correlación puede elevar progresivamente el riesgo y permitir pasar de:

**Nivel 1 — Enriquecimiento**

a:

**Nivel 2 — Recomendación**

y posteriormente:

**Nivel 3 — Contención automática reversible**

sin depender de una única señal.

## 4.8 Política de decisión

Una automatización debería evaluarse al menos con:

**Confianza de la UD**  
× **criticidad del activo o identidad**  
× **correlación con otras señales**  
× **impacto de la acción**  
× **reversibilidad**

Una detección frecuente no debe automatizarse únicamente porque sea fácil de ejecutar.

## 4.9 Controles de seguridad para automatización

Antes de habilitar una acción automática deben existir:

- listas de exclusión controladas;
- límites de duración del bloqueo;
- mecanismo de reversión;
- registro completo de la acción;
- trazabilidad entre UD y acción ejecutada;
- control de concurrencia;
- protección de activos críticos;
- criterios para escalamiento humano;
- pruebas en modo simulación;
- revisión periódica de efectividad.

## 4.10 Métrica de automatización

La v0.2 incorpora una dimensión adicional de cobertura:

> **Automation Coverage**

Puede medirse como la proporción de UD validadas que cuentan con una respuesta definida y, dentro de ellas, cuáles permiten automatización segura.

Ejemplo conceptual:

- UD diseñadas: 20
- UD implementadas: 15
- UD validadas: 12
- UD con respuesta definida: 10
- UD con enriquecimiento automático: 9
- UD con contención automática reversible: 4

El objetivo no es maximizar el número de acciones automáticas, sino automatizar aquellas donde el beneficio supera claramente el riesgo operativo.

## 4.11 Resultado esperado

El framework debe permitir representar una cadena como:

**Escenario**  
→ **Fase**  
→ **CD**  
→ **UD**  
→ **Telemetría**  
→ **Detección**  
→ **Correlación**  
→ **Decisión**  
→ **Acción automática o humana**

La automatización temprana se convierte así en una propiedad explícita de las UD y en un componente medible de la capacidad de respuesta.
