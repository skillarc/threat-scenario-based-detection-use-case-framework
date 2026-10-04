# Casos de uso basados en escenarios de amenaza

> **Threat Scenario-Based Detection Use Case Framework — Draft v0.2**

## ¿Qué son los casos de uso basados en escenarios de amenaza?

Los **casos de uso basados en escenarios de amenaza** son detecciones diseñadas a partir de la forma en que una amenaza puede materializarse y progresar dentro de una organización.

A diferencia de un enfoque centrado únicamente en reglas aisladas, eventos disponibles o funcionalidades de un SIEM, este modelo comienza identificando un **escenario de amenaza relevante**, descomponiéndolo en fases y comportamientos observables, y convirtiendo esos comportamientos en capacidades y unidades de detección.

Dentro de este framework, el objetivo no es crear la mayor cantidad posible de casos de uso. El objetivo es responder:

> **¿Qué escenario de amenaza necesito cubrir, dónde puedo observarlo, qué detecciones necesito, qué brechas existen y qué respuesta puedo ejecutar antes de que el ataque progrese?**

## Casos de uso de detección basados en escenarios de amenaza

La metodología organiza el diseño mediante la siguiente cadena:

**Objetivo / Riesgo**  
↓  
**Threat Intelligence / Contexto**  
↓  
**Escenario de amenaza**  
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
**MITRE ATT&CK**  
↓  
**Cobertura y gaps**  
↓  
**Respuesta / Automatización**  
↓  
**Validación y mejora continua**

## ¿Por qué diseñar casos de uso desde escenarios de amenaza?

Un catálogo tradicional de casos de uso puede crecer durante años sin demostrar necesariamente que una organización tenga cobertura adecuada frente a sus amenazas prioritarias.

Por ejemplo, una organización puede disponer de decenas de reglas relacionadas con autenticación y, aun así, carecer de visibilidad sobre otras fases de un escenario como reconocimiento, ejecución, movimiento lateral o exfiltración.

El enfoque basado en escenarios permite evaluar:

- qué amenazas se pretenden detectar;
- qué fases del ataque están cubiertas;
- qué comportamientos son observables;
- qué fuentes de datos son necesarias;
- qué detecciones existen realmente;
- qué gaps permanecen;
- qué acciones de respuesta pueden automatizarse.

## Casos de uso SIEM basados en escenarios de amenaza

El framework puede utilizarse para diseñar **casos de uso SIEM basados en escenarios de amenaza**, pero no depende de un SIEM específico.

Una Unidad de Detección puede implementarse en:

- SIEM;
- XDR;
- EDR;
- NDR;
- WAF;
- firewall;
- IAM;
- plataformas cloud;
- herramientas de identidad;
- sistemas de protección de datos.

El SIEM puede actuar como plataforma de correlación, pero la metodología permanece independiente del fabricante.

## Escenarios de amenaza y fases

La versión v0.2 utiliza cinco fases base:

1. **Reconocimiento**
2. **Acceso inicial**
3. **Ejecución / Acción**
4. **Persistencia / Movimiento lateral**
5. **Exfiltración / Impacto**

Estas fases permiten ordenar la progresión del escenario y medir cobertura.

No implican que todos los ataques deban seguir una secuencia estrictamente lineal.

## Capacidad de Detección (CD)

Una **Capacidad de Detección (CD)** expresa qué comportamiento o condición relevante necesita ser detectado.

Ejemplo:

> **CD — Detectar abuso de mecanismos de autenticación sobre servicios expuestos.**

La CD representa la necesidad metodológica, no una regla específica.

## Unidad de Detección (UD)

Una **Unidad de Detección (UD)** es la lógica específica, implementable, verificable y medible que materializa una parte de una CD.

Para la CD anterior podrían existir:

- UD — múltiples intentos fallidos desde un mismo origen;
- UD — múltiples usuarios atacados desde un mismo origen;
- UD — autenticación satisfactoria posterior a múltiples fallos;
- UD — autenticación desde geolocalización no habitual;
- UD — actividad fuera del patrón temporal esperado.

## Casos de uso y MITRE ATT&CK

MITRE ATT&CK puede utilizarse para relacionar las UD con tácticas, técnicas o subtécnicas conocidas.

El framework no utiliza MITRE ATT&CK como sustituto del escenario de amenaza.

La relación propuesta es:

**Escenario de amenaza**  
→ **Fase**  
→ **Comportamiento**  
→ **CD**  
→ **UD**  
→ **MITRE ATT&CK**

De esta forma, MITRE ATT&CK aporta trazabilidad sin obligar a diseñar las detecciones exclusivamente desde una matriz de técnicas.

## Casos de uso y fuentes de datos

Toda UD debe identificar la telemetría necesaria.

Ejemplos de fuentes:

- firewall;
- WAF;
- Active Directory;
- Entra ID;
- VPN;
- EDR/XDR;
- DNS;
- proxy;
- NDR;
- cloud logs;
- aplicaciones;
- sistemas de identidad.

Cuando la fuente no existe o la evidencia necesaria no está disponible, el framework registra un gap en lugar de asumir que la detección está cubierta.

## Casos de uso y automatización SOAR

Uno de los objetivos centrales del framework es conectar las UD con **respuesta y automatización**, especialmente durante las primeras fases:

**Reconocimiento → Acceso inicial**

Ejemplo conceptual:

**UD — Escaneo de puertos**  
→ enriquecimiento automático  
→ reputación / ASN / geolocalización  
→ correlación con otras UD  
→ incremento de riesgo  
→ bloqueo temporal cuando se cumplen criterios de confianza

Posteriormente:

**UD — Password Spray**  
→ identificación de usuarios afectados  
→ correlación con actividad previa  
→ bloqueo temporal de origen

Y si aparece:

**UD — Login satisfactorio posterior a múltiples fallos**  
→ elevar criticidad  
→ validar sesión  
→ revocar sesión o token bajo política autorizada  
→ investigación prioritaria

La automatización se diseña desde la UD y debe considerar confianza, criticidad, impacto y reversibilidad.

## Cobertura de casos de uso

La cobertura no debe medirse únicamente como número de reglas.

El framework propone evaluar:

- cobertura por escenario;
- cobertura por fase;
- cobertura por comportamiento;
- cobertura por CD;
- cobertura por UD;
- cobertura de telemetría;
- estado de validación;
- Automation Coverage.

## Tipos de gaps

El framework diferencia:

- **Detection Gap:** existe telemetría, pero falta una UD adecuada.
- **Telemetry Gap:** no existe una fuente que entregue la evidencia necesaria.
- **Visibility Gap:** la fuente existe, pero la información requerida no está habilitada o disponible.
- **Control / Architecture Gap:** la arquitectura limita la capacidad de observar, detectar o responder.

## Ejemplo resumido

### Escenario

**Compromiso de acceso remoto expuesto a Internet**

### Reconocimiento

- CD — Detectar reconocimiento activo sobre el servicio.
- UD — escaneo de múltiples puertos.
- UD — enumeración de portal VPN.
- UD — actividad desde infraestructura con reputación adversa.

### Acceso inicial

- CD — Detectar abuso de autenticación.
- UD — password spray.
- UD — brute force sobre una cuenta.
- UD — múltiples usuarios atacados desde un mismo origen.
- UD — login satisfactorio posterior a múltiples fallos.

### Automatización

- enriquecimiento automático;
- scoring de riesgo;
- bloqueo temporal de IP;
- seguimiento de usuarios afectados;
- cierre de sesión o revocación de token cuando corresponda;
- escalamiento humano ante acciones de mayor impacto.

## Términos relacionados

Esta metodología se relaciona con búsquedas y conceptos como:

- casos de uso basados en escenarios de amenaza;
- casos de uso basados en escenarios de amenazas;
- casos de uso de detección basados en escenarios de amenaza;
- casos de uso SIEM basados en escenarios de amenaza;
- diseño de casos de uso SIEM;
- framework de casos de uso de ciberseguridad;
- metodología de casos de uso para SOC;
- ingeniería de detección;
- detection engineering;
- threat modeling;
- threat-informed defense;
- MITRE ATT&CK;
- automatización SOAR;
- cobertura de detección;
- escenarios de amenaza en ciberseguridad.

## Nombre del framework

La metodología se publica como:

**Threat Scenario-Based Detection Use Case Framework**

Su propósito es proporcionar una forma estructurada y reproducible de transformar **escenarios de amenaza en casos de uso de detección, Capacidades de Detección (CD), Unidades de Detección (UD), cobertura medible y respuesta automatizable**.
