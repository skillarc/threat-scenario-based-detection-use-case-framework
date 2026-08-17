# 1. Introducción, problema, propósito y alcance

> **Threat Scenario-Based Detection Use Case Framework — Draft v0.1**

## 1.1 Introducción

Las capacidades de detección de seguridad suelen evolucionar a partir de reglas, eventos, firmas o correlaciones individuales. Este enfoque puede ser útil para resolver necesidades puntuales, pero también puede producir catálogos extensos de casos de uso cuya relación con amenazas concretas, rutas de ataque y objetivos de protección no siempre es evidente.

Estoy desarrollando el **Threat Scenario-Based Detection Use Case Framework** para abordar ese problema desde una perspectiva diferente: comenzar por el **escenario de amenaza** y utilizarlo como unidad principal de diseño, análisis y evaluación de la capacidad de detección.

El propósito no es únicamente responder a la pregunta *“¿qué regla puedo crear con los datos que ya tengo?”*, sino a una pregunta más amplia:

> **¿Qué escenario de amenaza necesito detectar, cómo puede evolucionar, qué comportamientos pueden observarse durante su desarrollo y qué capacidades necesito para detectar esas señales a tiempo?**

A partir de esta premisa, el framework busca conectar de forma trazable el contexto de amenaza con el modelado del escenario, las rutas de ataque, las oportunidades de detección, las fuentes de datos disponibles, los casos de uso de detección y la medición de cobertura y brechas.

## 1.2 Problema que busca resolver

En muchos entornos de monitoreo y CyberSOC, los casos de uso pueden desarrollarse de forma reactiva o impulsados principalmente por la disponibilidad de una fuente de datos, una funcionalidad del SIEM, una alerta de fabricante, una necesidad operativa puntual o un incidente previamente observado.

El resultado puede ser técnicamente válido y, al mismo tiempo, presentar varias limitaciones:

- dificultad para explicar qué escenario de amenaza justifica cada detección;
- escasa trazabilidad entre amenazas, comportamientos adversarios, fases de ataque y reglas implementadas;
- detecciones concentradas en determinadas fases mientras otras permanecen sin cobertura;
- dificultad para distinguir entre ausencia de una regla y ausencia de la telemetría necesaria para construirla;
- crecimiento del número de casos de uso sin una medida equivalente del incremento real de cobertura;
- priorización basada en disponibilidad tecnológica en lugar de relevancia de la amenaza;
- dependencia excesiva de una herramienta, fabricante o arquitectura específica;
- dificultad para traducir información de Threat Intelligence en decisiones concretas de Detection Engineering.

Por ello, **el número de casos de uso implementados no debería utilizarse por sí solo como medida de capacidad de detección**. Una organización puede disponer de cientos de reglas y continuar teniendo brechas importantes frente a un escenario crítico si dichas reglas se concentran en los mismos comportamientos o fases.

El framework propone cambiar la unidad de análisis: de la regla individual hacia la **cobertura del escenario de amenaza**.

## 1.3 Tesis central

La tesis principal del framework es:

> **El escenario de amenaza es la unidad principal de diseño y evaluación. Los casos de uso de detección son mecanismos de observación que, en conjunto, proporcionan cobertura sobre dicho escenario.**

Esta idea implica que un caso de uso no debería evaluarse únicamente por su funcionamiento técnico. También debería ser posible responder:

- ¿qué escenario de amenaza contribuye a detectar?;
- ¿qué comportamiento adversario observa?;
- ¿en qué fase o punto de la ruta de ataque puede manifestarse?;
- ¿qué evidencia o telemetría necesita?;
- ¿qué cobertura aporta?;
- ¿qué brecha permanece después de implementarlo?;

## 1.4 Propósito del framework

El propósito del **Threat Scenario-Based Detection Use Case Framework** es proporcionar una metodología estructurada para **transformar escenarios de amenaza relevantes en capacidades de detección trazables, medibles y mejorables**.

Para ello, el framework busca integrar de forma coherente:

**Threat Intelligence / Contexto**  
↓  
**Threat Scenario**  
↓  
**Threat Modeling**  
↓  
**Attack Path / Fases del ataque**  
↓  
**Detection Opportunities**  
↓  
**Data Sources / Telemetría**  
↓  
**Detection Use Cases**  
↓  
**Coverage & Gaps**  
↓  
**Improvement**

El resultado esperado no es siempre una nueva regla. Dependiendo del análisis, la mejora necesaria puede ser una nueva detección, una modificación de una detección existente, habilitación de logging, incorporación de una fuente de datos, normalización de telemetría, mejora de visibilidad o una modificación de arquitectura o controles.

## 1.5 Objetivo principal

El objetivo principal es:

> **Transformar escenarios de amenaza relevantes en capacidades de detección estructuradas, trazables y medibles mediante modelado de amenazas, análisis de rutas de ataque, identificación de oportunidades de detección y evaluación de la telemetría disponible.**

## 1.6 Objetivos específicos

El framework busca:

1. Diseñar capacidades de detección a partir de **escenarios de amenaza**, en lugar de depender únicamente de eventos o reglas aisladas.
2. Proporcionar trazabilidad entre **amenaza, escenario, comportamiento adversario, fase de ataque, fuente de datos y caso de uso de detección**.
3. Incorporar **Threat Intelligence** como entrada para seleccionar, contextualizar y priorizar escenarios relevantes.
4. Aplicar **Threat Modeling** para representar cómo un escenario puede materializarse y evolucionar.
5. Identificar **Detection Opportunities / Detection Points** antes de diseñar reglas específicas.
6. Determinar qué **telemetría** es necesaria para observar cada comportamiento relevante.
7. Diseñar y priorizar **Detection Use Cases** en función de la cobertura que aportan al escenario.
8. Relacionar comportamientos adversarios con marcos como **MITRE ATT&CK** cuando sea aplicable.
9. Medir la **cobertura por escenario y por fase de ataque**.
10. Identificar y diferenciar **Detection Gaps, Telemetry Gaps, Visibility Gaps y Control / Architecture Gaps**.
11. Utilizar las brechas identificadas para orientar decisiones de Detection Engineering y arquitectura de seguridad.
12. Facilitar una mejora continua basada en cambios de amenaza, infraestructura, telemetría y controles.
13. Mantener independencia respecto de fabricantes, tecnologías SIEM/XDR y sectores específicos.

## 1.7 Alcance

El framework está diseñado para ser **transversal a diferentes organizaciones e industrias**. Su aplicación no depende de una marca específica de SIEM, XDR, EDR, firewall, plataforma cloud u otra tecnología de seguridad.

El escenario de amenaza puede mantenerse conceptualmente estable entre organizaciones, mientras que las capacidades concretas de detección variarán según:

- arquitectura tecnológica;
- activos y servicios críticos;
- controles existentes;
- fuentes de datos disponibles;
- calidad y granularidad de la telemetría;
- capacidad de integración y normalización;
- contexto de amenaza de la organización;
- nivel de madurez del equipo de seguridad.

Por tanto, el framework no pretende que todas las organizaciones implementen exactamente los mismos casos de uso. Pretende que puedan aplicar un **proceso común para determinar qué necesitan detectar, qué pueden observar y qué brechas deben resolver**.

## 1.8 Fuera de alcance en esta etapa

En su versión inicial, el framework no pretende:

- sustituir marcos de inteligencia de amenazas;
- reemplazar MITRE ATT&CK u otras taxonomías de comportamiento adversario;
- sustituir metodologías completas de gestión de riesgos;
- imponer una única metodología de threat modeling;
- definir consultas específicas para un SIEM determinado como requisito del framework;
- establecer un modelo universal de puntuación de riesgo sin considerar el contexto organizacional;
- afirmar que la existencia de una regla equivale automáticamente a una detección efectiva.

Estos elementos pueden utilizarse como entradas, referencias o mecanismos complementarios dentro del proceso.

## 1.9 Resultados esperados

Una aplicación completa del framework debería permitir producir, como mínimo:

- un escenario de amenaza claramente definido;
- un modelo de cómo puede evolucionar;
- una representación de sus fases o rutas de ataque;
- comportamientos relevantes y oportunidades de detección;
- requisitos de telemetría asociados;
- casos de uso de detección vinculados al escenario;
- un mapa de cobertura;
- brechas identificadas y clasificadas;
- acciones de mejora priorizadas.

El objetivo final es que un equipo de seguridad pueda responder no solo **“qué detectamos”**, sino también **“qué amenaza estamos cubriendo, dónde la podemos detectar, qué tan completa es esa cobertura y qué necesitamos mejorar”**.

## 1.10 Evolución del framework

Esta especificación se encuentra en desarrollo. La terminología, métricas, artefactos y mecanismos de evaluación serán refinados mediante comparación con marcos existentes, revisión técnica y aplicación a escenarios prácticos.

El framework será contrastado, entre otros, con enfoques de **Threat-Informed Defense, Detection Engineering, MITRE ATT&CK, Cyber Kill Chain, threat modeling y gestión de casos de uso como MaGMa**, con el objetivo de identificar claramente qué componentes reutiliza, cuáles complementa y dónde existe una contribución diferenciada.
