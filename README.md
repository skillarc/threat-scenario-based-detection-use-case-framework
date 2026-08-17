# Threat Scenario-Based Detection Use Case Framework

> **Draft v0.1 — Work in Progress**

Estoy desarrollando **Threat Scenario-Based Detection Use Case Framework**, una metodología orientada a diseñar casos de uso de detección a partir de **escenarios de amenaza**, en lugar de construir detecciones como eventos o reglas aisladas.

La idea parte de una pregunta sencilla: **¿qué escenario de amenaza necesito detectar y qué visibilidad tengo para identificar su evolución?**

El framework busca establecer un proceso trazable que permita partir del contexto de amenazas, definir un escenario relevante, modelar cómo podría desarrollarse un ataque, identificar sus fases y comportamientos observables, y convertir esos puntos de detección en casos de uso que puedan implementarse mediante la telemetría disponible en cada organización.

## Concepto inicial

El flujo que estoy desarrollando considera, de manera preliminar:

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
**Data Sources / Telemetría disponible**  
↓  
**Detection Use Cases**  
↓  
**Coverage & Gaps**

Esto permite que los casos de uso tengan trazabilidad hacia un escenario concreto y que sea posible determinar **qué parte del escenario está cubierta, dónde existen brechas de visibilidad y qué nuevas capacidades de detección deberían desarrollarse**.

## Objetivo

Mi objetivo es construir un framework transversal que pueda adaptarse a organizaciones con diferentes tecnologías y niveles de madurez. El elemento central no debería ser una herramienta, un SIEM específico o una industria determinada, sino el **escenario de amenaza** y la capacidad real de la organización para observarlo.

Las fuentes de datos disponibles —firewalls, identidades, endpoints, servidores, nube, aplicaciones, redes u otras tecnologías— determinarán qué comportamientos pueden observarse y, por tanto, qué cobertura de detección puede alcanzarse frente al escenario modelado.

## Principios iniciales

- Diseñar detecciones a partir de **escenarios de amenaza**, no únicamente de eventos aislados.
- Utilizar **modelado de amenazas** para entender cómo puede desarrollarse cada escenario.
- Relacionar las detecciones con las diferentes **fases y comportamientos del ataque**.
- Identificar los **puntos de detección** antes de diseñar reglas específicas.
- Evaluar las **fuentes de datos y telemetría** realmente disponibles.
- Relacionar los comportamientos adversarios con marcos reconocidos como **MITRE ATT&CK** cuando corresponda.
- Medir la **cobertura y las brechas de detección** respecto del escenario completo.
- Mantener independencia respecto de fabricantes y tecnologías específicas.

## Estado del proyecto

Este repositorio contiene una metodología **en desarrollo**. La estructura, terminología, métricas y artefactos todavía están siendo definidos y podrán cambiar a medida que el framework sea contrastado con literatura, frameworks existentes y casos prácticos.

Como parte de este proceso, evaluaré su relación y diferencias con enfoques existentes de threat modeling, threat-informed defense, detection engineering y gestión de casos de uso, incluyendo referencias como **MITRE ATT&CK**, Cyber Kill Chain y **MaGMa Use Case Framework**.

La intención de esta primera publicación es documentar la evolución del enfoque de manera abierta y construir progresivamente una especificación reproducible.

---

**Threat Scenario-Based Detection Use Case Framework — Draft v0.1**