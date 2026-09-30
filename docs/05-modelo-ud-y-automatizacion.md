# 5. Modelo de Unidad de Detección y automatización

> **Threat Scenario-Based Detection Use Case Framework — Draft v0.2**

## 5.1 Objetivo

La Unidad de Detección (UD) es el elemento implementable del framework. Para que una UD pueda participar en respuesta automática debe documentar no solo su lógica de detección, sino también las condiciones bajo las cuales una acción puede ejecutarse de forma segura.

La automatización no debe depender únicamente de que una alerta se dispare.

## 5.2 Estructura mínima de una UD

| Campo | Descripción |
|---|---|
| ID | Identificador único de la UD |
| Nombre | Comportamiento específico que detecta |
| Escenario | Escenario(s) de amenaza al que contribuye |
| Fase | Reconocimiento, Acceso inicial, Ejecución/Acción, Persistencia/Movimiento lateral o Exfiltración/Impacto |
| CD | Capacidad de Detección asociada |
| Objetivo | Qué condición se busca observar |
| Comportamiento observable | Evidencia concreta que materializa la detección |
| Fuente de datos | Tecnología o sistema que genera la telemetría |
| Campos mínimos | Entidades necesarias para ejecutar la lógica |
| Ventana temporal | Intervalo utilizado para correlación |
| Lógica | Condiciones, secuencias, umbrales o correlaciones |
| Exclusiones | Actividad autorizada o condiciones que deben omitirse |
| MITRE ATT&CK | Técnica/subtécnica cuando exista correspondencia válida |
| Evidencia | Datos que debe recibir el analista |
| Confianza | Baja, media o alta, sustentada por validación |
| Criticidad | Impacto potencial del comportamiento |
| Estado de validación | Diseñada, implementada, probada, validada |
| Acción recomendada | Respuesta asociada |
| Nivel de automatización | 0 a 4 |
| Reversibilidad | Cómo revertir la acción |
| TTL | Duración de una contención temporal |
| Condiciones de escalamiento | Cuándo requiere intervención humana |

## 5.3 Estados de madurez de una UD

Una UD puede recorrer los siguientes estados:

**Diseñada**  
→ **Implementada**  
→ **Probada**  
→ **Validada**  
→ **Respuesta definida**  
→ **Automatización en simulación**  
→ **Automatización controlada**  
→ **Automatización operativa**

Una UD no debe pasar directamente de diseño a respuesta automática.

## 5.4 Elegibilidad para automatización

Una UD es candidata a automatización cuando cumple, como mínimo:

1. telemetría estable;
2. campos críticos disponibles;
3. lógica probada;
4. tasa de falsos positivos conocida;
5. exclusiones controladas;
6. entidad objetivo claramente identificada;
7. acción definida;
8. acción reversible o de impacto aceptable;
9. registro completo de la acción;
10. mecanismo de escalamiento humano.

## 5.5 Decisión de automatización

El framework propone separar cuatro preguntas:

### ¿La UD detecta con suficiente confianza?

Si no existe suficiente confianza, debe mantenerse en observación o enriquecimiento.

### ¿La acción tiene bajo impacto?

Las acciones de bajo impacto pueden automatizarse antes que aquellas capaces de interrumpir servicios o usuarios críticos.

### ¿La acción es reversible?

Una acción temporal y reversible reduce el riesgo operacional.

### ¿Existen señales adicionales?

La correlación entre varias UD puede elevar el nivel de confianza y habilitar una respuesta más fuerte.

## 5.6 Modelo de decisión

La decisión puede representarse conceptualmente como:

**UD activada**  
↓  
**Validar exclusiones**  
↓  
**Enriquecer entidad**  
↓  
**Correlacionar con otras UD**  
↓  
**Calcular nivel de confianza**  
↓  
**Evaluar criticidad del activo / identidad**  
↓  
**Seleccionar acción permitida**  
↓  
**Ejecutar o solicitar aprobación**  
↓  
**Registrar resultado**  
↓  
**Reevaluar**

## 5.7 Perfil de automatización para Reconocimiento

Las UD de Reconocimiento deberían priorizar:

- enriquecimiento automático;
- reputación de IP/dominio;
- geolocalización y ASN;
- clasificación del activo objetivo;
- watchlists;
- incremento de riesgo;
- rate limiting;
- bloqueo temporal de origen cuando existe correlación suficiente.

La respuesta debe evitar medidas de alto impacto basadas únicamente en una señal aislada de reconocimiento.

## 5.8 Perfil de automatización para Acceso inicial

Las UD de Acceso inicial pueden admitir acciones más fuertes cuando existe evidencia de progresión.

Ejemplos:

### Password spray

**UD:** un origen intenta autenticarse contra múltiples usuarios.

**Respuesta inicial:**

- enriquecer origen;
- comprobar exclusiones;
- correlacionar reputación;
- identificar usuarios afectados;
- bloquear temporalmente el origen si se supera el criterio de confianza.

### Éxito posterior a múltiples fallos

**UD:** autenticación satisfactoria relacionada con una secuencia de fallos.

**Respuesta inicial:**

- elevar criticidad;
- identificar sesión y usuario;
- correlacionar dispositivo, IP y geolocalización;
- cerrar sesión o revocar token cuando la política lo permita;
- forzar validación adicional;
- iniciar investigación prioritaria.

## 5.9 Correlación progresiva

El framework busca que las primeras fases puedan construir una señal compuesta.

Ejemplo:

**UD-R01 — Escaneo de puertos**  
↓  
**UD-R02 — Enumeración de servicio VPN**  
↓  
**UD-A01 — Password spray**  
↓  
**UD-A02 — Login satisfactorio posterior a fallos**

Cada UD agrega contexto.

La política de respuesta puede definir:

- 1 UD: observar y enriquecer;
- 2 UD correlacionadas: elevar riesgo y recomendar acción;
- 3 o más UD correlacionadas: ejecutar contención reversible si se cumplen los criterios de confianza.

Este esquema es conceptual y debe adaptarse al contexto de cada organización.

## 5.10 Métricas por UD

Además de métricas tradicionales de detección, una UD debería poder medir:

- activaciones;
- verdaderos positivos;
- falsos positivos;
- tiempo hasta enriquecimiento;
- tiempo hasta decisión;
- tiempo hasta contención;
- acciones automáticas ejecutadas;
- acciones revertidas;
- bloqueos incorrectos;
- porcentaje de activaciones que requirió intervención humana.

## 5.11 Objetivo de la automatización

El objetivo no es automatizar la mayor cantidad posible de UD.

El objetivo es lograr que **las señales con mayor confianza puedan producir una respuesta proporcional antes de que el escenario alcance fases de mayor impacto**.

Por ello, la v0.2 considera especialmente valiosa la automatización de UD en:

**Reconocimiento → Acceso inicial**

cuando la acción sea controlable, trazable y reversible.
