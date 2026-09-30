# 3. Modelo metodológico v0.2

> **Threat Scenario-Based Detection Use Case Framework — Draft v0.2**

## 3.1 Flujo metodológico

La versión v0.2 organiza el framework en el siguiente flujo:

**Objetivo / Riesgo**  
↓  
**Threat Intelligence / Contexto**  
↓  
**Escenario de Amenaza**  
↓  
**Threat Modeling**  
↓  
**Fases del escenario**  
↓  
**Comportamientos adversarios**  
↓  
**Capacidades de Detección (CD)**  
↓  
**Unidades de Detección (UD)**  
↓  
**Fuentes de datos / Telemetría**  
↓  
**Lógica de detección**  
↓  
**MITRE ATT&CK / Trazabilidad**  
↓  
**Cobertura y Gaps**  
↓  
**Respuesta / Automatización**  
↓  
**Validación y mejora continua**

## 3.2 Paso 1 — Definir el objetivo o riesgo

El proceso comienza identificando qué se necesita proteger o qué riesgo se desea reducir.

El objetivo no debe expresarse como una tecnología, por ejemplo “monitorear el firewall”, sino como una necesidad de seguridad, por ejemplo:

> Detectar y contener intentos de compromiso sobre servicios de acceso remoto expuestos a Internet antes de que se produzca una intrusión efectiva.

## 3.3 Paso 2 — Incorporar contexto de amenaza

Threat Intelligence aporta contexto para:

- identificar actores y campañas relevantes;
- conocer TTP observadas;
- entender vectores de acceso;
- reconocer infraestructura o indicadores adversarios;
- priorizar escenarios.

La inteligencia no determina por sí sola la detección. Funciona como una entrada para construir escenarios relevantes.

## 3.4 Paso 3 — Definir el escenario de amenaza

El escenario debe describir:

- qué intenta lograr el adversario;
- sobre qué superficie;
- mediante qué rutas plausibles;
- qué activos pueden verse afectados;
- qué condiciones permiten el avance;
- qué comportamientos podrían observarse.

## 3.5 Paso 4 — Modelar la progresión

Se identifican caminos plausibles de evolución del escenario y se asignan a las fases:

1. Reconocimiento
2. Acceso inicial
3. Ejecución / Acción
4. Persistencia / Movimiento lateral
5. Exfiltración / Impacto

El modelo puede contener rutas alternativas y bifurcaciones.

## 3.6 Paso 5 — Identificar comportamientos observables

Cada fase debe descomponerse en comportamientos suficientemente específicos para ser observables.

Ejemplos:

- escaneo de múltiples puertos;
- enumeración de servicios publicados;
- múltiples intentos de autenticación;
- autenticación posterior a una secuencia de fallos;
- ejecución de software no autorizado;
- uso anómalo de credenciales privilegiadas;
- acceso lateral entre servidores;
- transferencia inusual de información.

## 3.7 Paso 6 — Definir Capacidades de Detección

Los comportamientos se agrupan en CD.

Una CD representa lo que la organización necesita ser capaz de detectar, independientemente de la implementación.

Ejemplo:

**CD: Detectar reconocimiento activo sobre servicios expuestos.**

## 3.8 Paso 7 — Diseñar Unidades de Detección

Cada CD se materializa en una o más UD.

Ejemplo:

**CD: Detectar reconocimiento activo sobre servicios expuestos**

- UD: múltiples conexiones a puertos diferentes desde un mismo origen;
- UD: incremento anómalo de conexiones denegadas desde un mismo origen;
- UD: enumeración de múltiples servicios publicados;
- UD: actividad desde infraestructura con reputación adversa combinada con patrón de reconocimiento.

## 3.9 Paso 8 — Validar telemetría

Por cada UD debe comprobarse:

1. qué fuente genera la evidencia;
2. si la fuente está integrada;
3. si se reciben los campos mínimos;
4. si la granularidad es suficiente;
5. si el tiempo de ingesta permite respuesta;
6. si existen brechas de visibilidad.

Si la telemetría no existe, no debe forzarse la creación de la UD: debe registrarse el gap correspondiente.

## 3.10 Paso 9 — Implementar la lógica

La lógica concreta puede implementarse en SIEM, XDR, EDR, NDR, WAF, firewall, IAM u otra plataforma.

El framework permanece independiente del lenguaje de consulta.

La implementación debería registrar:

- condiciones;
- umbrales;
- ventanas temporales;
- entidades;
- exclusiones;
- correlaciones;
- evidencia requerida;
- criterios de cierre.

## 3.11 Paso 10 — Mapear MITRE ATT&CK

MITRE ATT&CK aporta una taxonomía para relacionar comportamientos observados con tácticas y técnicas conocidas.

El mapeo debe realizarse sobre el comportamiento real observado y no únicamente sobre el nombre de la alerta.

## 3.12 Paso 11 — Medir cobertura y gaps

La medición mínima debe responder:

- ¿qué fases están cubiertas?;
- ¿qué comportamientos tienen CD?;
- ¿qué CD tienen UD implementadas?;
- ¿qué UD poseen telemetría suficiente?;
- ¿qué UD fueron validadas?;
- ¿qué partes del escenario permanecen sin visibilidad?;
- ¿qué detecciones permiten respuesta automática?

## 3.13 Paso 12 — Diseñar respuesta y automatización

Cada UD debe evaluarse para determinar si puede accionar:

- enriquecimiento;
- notificación;
- bloqueo;
- aislamiento;
- cierre de sesión;
- suspensión temporal;
- renovación de tokens;
- bloqueo geográfico;
- regla temporal de firewall/WAF;
- contención EDR;
- escalamiento a investigación.

La automatización no se agrega al final. Se diseña junto con la UD.

## 3.14 Paso 13 — Validar

La validación debe comprobar:

- que el comportamiento puede observarse;
- que la lógica detecta el patrón esperado;
- que el nivel de falsos positivos es aceptable;
- que la evidencia permite investigación;
- que una acción automatizada no produce un impacto operativo desproporcionado;
- que existe reversibilidad cuando corresponda.

## 3.15 Paso 14 — Mejorar

Los resultados deben retroalimentar:

- nuevas CD;
- nuevas UD;
- ajustes de lógica;
- nuevas fuentes;
- mejoras de telemetría;
- cambios de arquitectura;
- nuevas automatizaciones;
- actualización del escenario.

## 3.16 Resultado esperado

La salida del framework no es un catálogo de reglas.

La salida es un **mapa trazable de capacidad de detección y respuesta**, donde puede observarse cómo cada UD contribuye a detectar y, cuando sea seguro, contener una parte específica de un escenario de amenaza.
