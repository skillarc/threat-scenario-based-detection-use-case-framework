# Threat Scenario-Based Detection Use Case Framework

> **Draft v0.2 — Work in Progress**

**English summary:** A vendor-neutral, threat-informed **Detection Engineering** methodology for transforming **threat scenarios** into measurable **Detection Capabilities (CD)** and implementable **Detection Units (UD)**, mapping them to **data sources, telemetry and MITRE ATT&CK**, measuring **detection coverage and gaps**, and enabling controlled **SOC/SIEM/SOAR response automation** in the earliest attack phases.

**Resumen:** metodología para diseñar detecciones desde escenarios de amenaza, medir cobertura real y conectar cada Unidad de Detección con telemetría, contexto, respuesta y automatización.

## Áreas relacionadas / Related domains

**Threat Modeling · Threat-Informed Defense · Detection Engineering · Security Operations (SOC) · SIEM · SOAR · MITRE ATT&CK · Detection Coverage · Detection Gaps · Telemetry Engineering · Detection Automation · Incident Response · Use Case Management**

Estoy desarrollando **Threat Scenario-Based Detection Use Case Framework**, una metodología orientada a diseñar, medir y mejorar capacidades de detección a partir de **escenarios de amenaza**, en lugar de construir detecciones como eventos o reglas aisladas.

La idea parte de una pregunta sencilla: **¿qué escenario de amenaza necesito detectar, cómo puede evolucionar y qué visibilidad tengo para identificarlo a lo largo de sus distintas fases?**

El framework busca establecer un proceso trazable que permita partir del contexto de amenazas, definir un escenario relevante, modelar cómo podría desarrollarse un ataque, identificar sus fases y comportamientos observables, evaluar las fuentes de datos disponibles y convertir esos puntos de observación en capacidades de detección medibles.

## Diferenciadores del enfoque

- El **escenario de amenaza** es la unidad principal de diseño y evaluación.
- Separa **Capacidad de Detección (CD)** de **Unidad de Detección (UD)** para distinguir necesidad metodológica de lógica implementable.
- Mide cobertura por **escenario, fase, comportamiento, CD y UD**, en lugar de utilizar únicamente el número de reglas.
- Diferencia **Detection Gap, Telemetry Gap, Visibility Gap y Control / Architecture Gap**.
- Diseña la **respuesta y automatización desde la UD**, con énfasis en Reconocimiento y Acceso inicial.
- Mantiene independencia de fabricantes, SIEM, XDR, EDR y tecnologías específicas.

## Modelo v0.2

La versión v0.2 formaliza un flujo que conecta riesgo, amenaza, detección y respuesta:

**Objetivo / Riesgo**  
↓  
**Threat Intelligence / Contexto**  
↓  
**Threat Scenario**  
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
**Data Sources / Telemetría**  
↓  
**Lógica de detección**  
↓  
**MITRE ATT&CK / Trazabilidad**  
↓  
**Coverage & Gaps**  
↓  
**Response / Automation**  
↓  
**Validation & Improvement**

La finalidad no es únicamente generar casos de uso. El objetivo es entender **qué parte de un escenario puede observarse, qué parte puede detectarse, dónde existen brechas y qué capacidades deberían incorporarse o mejorarse**.

El escenario de amenaza se considera la unidad principal de diseño. Las **Capacidades de Detección (CD)** expresan qué se necesita ser capaz de detectar y las **Unidades de Detección (UD)** materializan esas capacidades mediante lógicas específicas, verificables y medibles.

## Objetivo principal

Mi objetivo es construir un framework transversal para **transformar escenarios de amenaza relevantes en capacidades de detección estructuradas, trazables y medibles**, mediante modelado de amenazas, análisis de rutas de ataque, identificación de oportunidades de detección y evaluación de la telemetría disponible.

El elemento central no debería ser una herramienta, un SIEM específico o una industria determinada, sino el **escenario de amenaza** y la capacidad real de la organización para observar y detectar su evolución.

## Documentación

La especificación formal se irá desarrollando progresivamente en la carpeta `docs/`.

- [1. Introducción, problema, propósito y alcance](docs/01-introduccion-problema-proposito-alcance.md)
- [2. Principios y terminología: CD y UD](docs/02-principios-y-terminologia.md)
- [3. Modelo metodológico v0.2](docs/03-modelo-metodologico-v0.2.md)
- [4. Fases y automatización temprana](docs/04-fases-y-automatizacion-temprana.md)
- [5. Modelo de Unidad de Detección y automatización](docs/05-modelo-ud-y-automatizacion.md)
- [6. English overview](docs/06-english-overview.md)
- [Roadmap](ROADMAP.md)
- [Changelog](CHANGELOG.md)
- [Contributing](CONTRIBUTING.md)

## Objetivos específicos

El framework busca:

- Cambiar el enfoque desde **detecciones aisladas hacia cobertura de escenarios de amenaza completos**.
- Proporcionar trazabilidad entre **amenaza, escenario, comportamiento adversario, fase, CD, UD, fuente de datos, lógica de detección y acción de respuesta**.
- Incorporar **Threat Intelligence** como una entrada para seleccionar y contextualizar escenarios relevantes.
- Incorporar **Threat Modeling** para comprender cómo puede materializarse y evolucionar cada escenario.
- Identificar **Detection Opportunities / Detection Points** antes de diseñar reglas o correlaciones específicas.
- Evaluar las **fuentes de datos y telemetría** necesarias para observar cada comportamiento relevante.
- Diseñar **Capacidades de Detección (CD)** y **Unidades de Detección (UD)** en función de la cobertura que aportan sobre el escenario.
- Relacionar comportamientos adversarios con marcos reconocidos como **MITRE ATT&CK** cuando corresponda.
- Medir la **cobertura de detección por escenario y por fase de ataque**.
- Identificar y diferenciar brechas de detección, telemetría, visibilidad y arquitectura.
- Utilizar esas brechas para orientar nuevas detecciones, mejoras de logging, incorporación de fuentes de datos o cambios de arquitectura de seguridad.
- Mantener independencia respecto de fabricantes, plataformas SIEM/XDR y tecnologías específicas.
- Facilitar la revisión y mejora continua cuando cambien las amenazas, la infraestructura o la capacidad de observación de la organización.
- Diseñar la **respuesta y automatización desde la UD**, priorizando acciones tempranas, controladas y reversibles durante Reconocimiento y Acceso inicial.

## Modelo inicial de cobertura y brechas

Una parte importante del framework será diferenciar por qué un comportamiento relevante no está cubierto.

De manera preliminar se consideran las siguientes categorías:

- **Detection Gap:** existe telemetría suficiente, pero no existe una capacidad de detección adecuada.
- **Telemetry Gap:** no existe una fuente de datos capaz de proporcionar la evidencia necesaria.
- **Visibility Gap:** la fuente existe, pero la información necesaria no está habilitada, recolectada, normalizada o disponible para análisis.
- **Control / Architecture Gap:** la arquitectura o los controles existentes limitan la capacidad de observar o detectar el comportamiento.

Esto permitirá que el resultado del framework no sea siempre la creación de un nuevo caso de uso. Dependiendo del gap identificado, el resultado puede ser también una recomendación de habilitación de logging, incorporación de telemetría, integración de una nueva fuente o mejora de arquitectura.

## Ciclo conceptual

El modelo puede resumirse inicialmente como:

**THREAT**  
↓  
**UNDERSTAND** — Threat Intelligence / Context  
↓  
**MODEL** — Threat Scenario / Threat Modeling / Attack Path  
↓  
**OBSERVE** — Detection Opportunities  
↓  
**VERIFY** — Data Sources / Telemetry  
↓  
**DESIGN** — Detection Capabilities (CD) / Detection Units (UD)  
↓  
**MEASURE** — Coverage & Gaps  
↓  
**RESPOND** — Human Response / Automation  
↓  
**IMPROVE** — Detection / Telemetry / Visibility / Architecture

## Principios iniciales

- Diseñar detecciones a partir de **escenarios de amenaza**, no únicamente de eventos aislados.
- Considerar el **escenario de amenaza como unidad principal de diseño y evaluación**.
- Utilizar **modelado de amenazas** para entender cómo puede desarrollarse cada escenario.
- Relacionar las detecciones con las diferentes **fases y comportamientos del ataque**.
- Identificar los **puntos de detección** antes de diseñar reglas específicas.
- Separar el nivel metodológico (**CD**) del nivel implementable (**UD**).
- Evaluar cada UD para determinar su capacidad de **enriquecimiento, recomendación o contención automatizada**.
- Evaluar las **fuentes de datos y telemetría** realmente disponibles.
- Relacionar los comportamientos adversarios con marcos reconocidos como **MITRE ATT&CK** cuando corresponda.
- Medir la **cobertura y las brechas de detección** respecto del escenario completo.
- Diferenciar entre falta de detección y falta de capacidad de observación.
- Utilizar los gaps identificados como entrada para la **mejora continua de detecciones y arquitectura de seguridad**.
- Mantener independencia respecto de fabricantes y tecnologías específicas.

## Estado del proyecto

Este repositorio contiene una metodología **en desarrollo**. La versión **v0.2** formaliza CD/UD, las cinco fases base del escenario, la trazabilidad con telemetría y una primera arquitectura de automatización temprana orientada a actuar sobre UD de Reconocimiento y Acceso inicial.

Como parte de este proceso, evaluaré su relación y diferencias con enfoques existentes de threat modeling, threat-informed defense, detection engineering y gestión de casos de uso, incluyendo referencias como **MITRE ATT&CK**, Cyber Kill Chain y **MaGMa Use Case Framework**.

La intención de esta publicación es documentar la evolución del enfoque de manera abierta y construir progresivamente una especificación reproducible.

---

**Threat Scenario-Based Detection Use Case Framework — Draft v0.2**