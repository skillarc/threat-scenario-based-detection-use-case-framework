# 2. Principios y terminología

> **Threat Scenario-Based Detection Use Case Framework — Draft v0.2**

## 2.1 Propósito de esta versión

La versión v0.2 formaliza la separación entre el nivel metodológico y el nivel implementable de la detección. El framework deja de utilizar el caso de uso como única unidad de diseño y adopta dos niveles complementarios:

- **Capacidad de Detección (CD):** capacidad metodológica que expresa qué comportamiento, condición o manifestación de un escenario de amenaza se necesita detectar.
- **Unidad de Detección (UD):** lógica específica, implementable, verificable y medible que materializa una parte de una Capacidad de Detección.

Esta separación permite evitar que una regla individual sea interpretada como una capacidad completa.

## 2.2 Principios de diseño

1. **El escenario de amenaza es la unidad principal de diseño y evaluación.**
2. **La cobertura se mide sobre el escenario y sus fases, no por cantidad de reglas.**
3. **Las CD representan capacidades; las UD representan implementaciones concretas.**
4. **Una CD puede contener múltiples UD.**
5. **Una UD puede contribuir a más de un escenario cuando observa un comportamiento reutilizable.**
6. **Toda UD debe tener evidencia observable y una fuente de telemetría identificable.**
7. **MITRE ATT&CK se utiliza como taxonomía de comportamiento y trazabilidad, no como sustituto del escenario.**
8. **La ausencia de detección debe clasificarse antes de crear una nueva regla.**
9. **La respuesta debe diseñarse junto con la detección, no como una etapa aislada posterior.**
10. **La automatización debe ser proporcional a la confianza de la detección, el impacto de la acción y la reversibilidad del control.**

## 2.3 Escenario de amenaza

Un **Escenario de Amenaza** describe una situación adversaria relevante para la organización, incluyendo:

- objetivo o efecto esperado del adversario;
- activos o servicios potencialmente afectados;
- condiciones de exposición;
- posibles rutas de ataque;
- comportamientos observables;
- fases de progresión;
- capacidades de detección necesarias;
- posibles acciones de respuesta.

Un escenario no debe reducirse a una técnica de MITRE ATT&CK ni a una alerta de una herramienta específica.

## 2.4 Fases del escenario

La versión v0.2 adopta como modelo base las siguientes fases:

1. **Reconocimiento**
2. **Acceso inicial**
3. **Ejecución / Acción**
4. **Persistencia / Movimiento lateral**
5. **Exfiltración / Impacto**

Las fases sirven para ordenar la progresión del escenario y medir cobertura. No obligan a que todos los ataques sigan una secuencia estrictamente lineal.

## 2.5 Capacidad de Detección (CD)

Una CD responde principalmente a:

> **¿Qué comportamiento o condición relevante necesito ser capaz de detectar dentro del escenario?**

Una CD debe ser:

- independiente de una consulta o lenguaje SIEM específico;
- suficientemente amplia para agrupar varias lógicas relacionadas;
- trazable a uno o más escenarios;
- asignable a una o más fases;
- verificable mediante UD concretas.

### Ejemplo conceptual

**CD — Detectar actividad anómala de autenticación sobre servicios expuestos.**

Esta capacidad puede materializarse mediante varias UD, por ejemplo:

- múltiples fallos desde un mismo origen;
- múltiples usuarios atacados desde un mismo origen;
- autenticación satisfactoria posterior a una secuencia de fallos;
- autenticación desde una geolocalización no habitual;
- autenticación fuera del patrón temporal esperado.

## 2.6 Unidad de Detección (UD)

Una UD responde principalmente a:

> **¿Qué lógica concreta utilizaré para observar un comportamiento específico y generar una señal accionable?**

Una UD debería documentar como mínimo:

- identificador;
- nombre;
- objetivo;
- escenario(s) relacionado(s);
- fase(s);
- CD asociada;
- comportamiento observable;
- fuente(s) de datos;
- campos mínimos requeridos;
- lógica de detección;
- ventana temporal;
- condiciones y umbrales;
- exclusiones;
- evidencias esperadas;
- mapeo MITRE ATT&CK cuando corresponda;
- criticidad;
- nivel de confianza;
- acción de respuesta recomendada;
- elegibilidad para automatización;
- estado de validación.

## 2.7 Relación entre CD y UD

La relación base es:

**Escenario de amenaza**  
→ **Fase**  
→ **Comportamiento adversario**  
→ **Capacidad de Detección (CD)**  
→ **Unidad(es) de Detección (UD)**  
→ **Telemetría**  
→ **Lógica de detección**  
→ **Respuesta / Automatización**

Una CD sin UD implementadas representa una capacidad requerida pero no materializada.

Una UD sin CD ni escenario asociado puede ser técnicamente válida, pero carece de contexto metodológico suficiente para medir su contribución a la cobertura.

## 2.8 Telemetría

La telemetría representa la evidencia necesaria para materializar una UD.

El framework diferencia entre:

- **fuente disponible:** la tecnología existe;
- **telemetría recolectada:** los eventos llegan a la plataforma de análisis;
- **telemetría utilizable:** contiene los campos y calidad necesarios;
- **telemetría accionable:** permite generar una UD confiable y soportar una decisión de respuesta.

## 2.9 Cobertura

La cobertura no debe expresarse únicamente como número de UD habilitadas.

La versión v0.2 propone medir, como mínimo:

- cobertura por escenario;
- cobertura por fase;
- cobertura por comportamiento;
- cobertura por CD;
- disponibilidad de telemetría;
- nivel de automatización alcanzable.

## 2.10 Gaps

Se mantienen las siguientes categorías:

- **Detection Gap:** existe telemetría suficiente, pero no existe una UD adecuada.
- **Telemetry Gap:** no existe una fuente capaz de entregar la evidencia requerida.
- **Visibility Gap:** la fuente existe, pero los datos necesarios no están disponibles, habilitados o normalizados.
- **Control / Architecture Gap:** la arquitectura o controles limitan la capacidad de observar, detectar o responder.

## 2.11 Automatización

La automatización forma parte de la capacidad de detección y respuesta.

Una UD puede clasificarse como:

- **Nivel 0 — Observación:** genera visibilidad, sin acción automática.
- **Nivel 1 — Enriquecimiento automático:** recopila contexto y evidencia.
- **Nivel 2 — Recomendación automática:** propone una acción, pero requiere aprobación humana.
- **Nivel 3 — Contención automática reversible:** ejecuta una acción preautorizada y reversible.
- **Nivel 4 — Respuesta automática de alto impacto:** reservada para condiciones con alta confianza, controles de seguridad y gobernanza explícita.

La meta de la v0.2 es permitir que determinadas UD de las primeras fases del escenario activen respuestas tempranas antes de que el adversario alcance fases de mayor impacto.
