# Biblioteca de Prompts

Este índice centraliza todos los prompts disponibles en el repositorio. El objetivo es facilitar la búsqueda, reutilización y evolución de estos prompts, manteniendo un estándar de documentación consistente.

---

## Índice rápido

| Título | Categoría | Archivo |
|--------|-----------|---------|
| [Diagrama de arquitectura HTML desde múltiples proyectos](#diagrama-de-arquitectura-html-desde-múltiples-proyectos) | writing | [ver](writing/writing-coding-architecture-diagram.md) |
| [Technical Decision Document Facilitator](#technical-decision-document-facilitator) | writing | [ver](writing/writing-technical-decisions.md) |
| [Strategic Initiative Facilitator (Spark)](#strategic-initiative-facilitator-spark) | writing | [ver](writing/writing-initiative-insight.md) |
| [Prompt Engineering Best Practices — System Prompt](#prompt-engineering-best-practices--system-prompt) | writing | [ver](writing/writing-meta-prompt.md) |
| [Post-Mortem Incident Report Writer](#post-mortem-incident-report-writer) | writing | [ver](writing/writing-post-mortem.md) |
| [Product Backlog Planner (Scrum Elements)](#product-backlog-planner-scrum-elements) | product | [ver](product/product-scrum-elements.md) |
| [User Story Enricher (Jira)](#user-story-enricher-jira) | product | [ver](product/product-enrich-user-story.md) |

---

## Catálogo detallado

### Diagrama de arquitectura HTML desde múltiples proyectos

**Categoría:** writing · **Versión:** 1.0.0 · **Autor:** ivan.loyarte · **Actualizado:** 2026-06-03

**Tags:** architecture, diagram, html, multi-repo, reverse-engineering

**Descripción:** Genera un diagrama de arquitectura HTML auto-contenido a partir de un directorio con
múltiples proyectos del mismo dominio. Escanea el stack tecnológico, conexiones entre servicios,
mensajería, bases de datos y endpoints expuestos; clasifica cada proyecto en capas (Frontend, BFF,
Gateway, Service, Data, Infra, External); y produce un archivo `architecture-diagram.html` con tema
oscuro (Tokyo Night), swimlanes por capa y cards con conexiones cruzadas.

📄 [writing-coding-architecture-diagram.md](writing/writing-coding-architecture-diagram.md)

---

### Technical Decision Document Facilitator

**Categoría:** writing · **Versión:** 1.0.0 · **Autor:** Diego Ravasani · **Actualizado:** 2026-04-09

**Tags:** architecture, decision-making, documentation, technical

**Descripción:** Guía al usuario en la creación de un Documento de Decisión Técnica sección
por sección. Útil para documentar decisiones de arquitectura, elección de tecnologías
o cualquier trade-off técnico que requiera justificación estructurada.

📄 [writing-technical-decisions.md](writing/writing-technical-decisions.md)

---

### Strategic Initiative Facilitator (Spark)

**Categoría:** writing · **Versión:** 1.0.0 · **Autor:** Diego Ravasani · **Actualizado:** 2026-04-09

**Tags:** strategy, documentation, facilitation, initiatives

**Descripción:** Transforma ideas en iniciativas documentadas y estructuradas. Guía al usuario
a través de un modelo de tres partes: problema, impacto esperado y descripción funcional.
Útil para documentar iniciativas técnicas, de producto o de negocio de forma rápida y consistente.

📄 [writing-initiative-insight.md](writing/writing-initiative-insight.md)

---

### Prompt Engineering Best Practices — System Prompt

**Categoría:** writing · **Versión:** 1.0.0 · **Autor:** Diego Ravasani · **Actualizado:** 2026-04-09

**Tags:** prompt-engineering, best-practices, llm, system-prompt

**Descripción:** Toma un prompt existente y lo reestructura aplicando las mejores prácticas de
ingeniería de prompts (rol, objetivo, formato, etc.) para lograr un resultado más preciso y
completo. Útil para mejorar la calidad y claridad de cualquier prompt respetando estrictamente
el objetivo original.

📄 [writing-meta-prompt.md](writing/writing-meta-prompt.md)

---

### Post-Mortem Incident Report Writer

**Categoría:** writing · **Versión:** 1.1.0 · **Autor:** Diego Ravasani · **Actualizado:** 2026-06-05

**Tags:** post-mortem, incident, documentation, ops

**Descripción:** Asistente especializado en la creación de informes post-mortem de incidentes de forma estructurada. 
Guía al usuario a través de una entrevista secuencial para capturar toda la información necesaria (síntoma, causa raíz, 
solución, detalle y plan de acción). Útil para documentar incidentes técnicos de manera consistente y completa, 
facilitando el aprendizaje organizacional y la prevención de recurrencias.

📄 [writing-post-mortem.md](writing/writing-post-mortem.md)

---

### Product Backlog Planner (Scrum Elements)

**Categoría:** product · **Versión:** 1.0.0 · **Autor:** Diego Ravasani · **Actualizado:** 2026-04-13

**Tags:** product, scrum, backlog, jira, user-stories, epics

**Descripción:** Guía al usuario en la estructuración de un requerimiento en épicas, historias de usuario y
tareas técnicas listas para ser creadas en un tablero de Jira. Solicita el nombre del proyecto,
la épica padre y las dependencias para generar ítems de backlog accionables y bien formateados.

📄 [product-scrum-elements.md](product/product-scrum-elements.md)

---

### User Story Enricher (Jira)

**Categoría:** product · **Versión:** 1.0.0 · **Autor:** Diego Ravasani · **Actualizado:** 2026-04-14

**Tags:** product, jira, user-stories, refinement, backlog, enrichment

**Descripción:** Analiza un ticket de Jira y determina si la historia de usuario cuenta con el nivel de detalle
técnico y funcional necesario para que un desarrollador la complete de forma autónoma. Si detecta
deficiencias, genera una versión mejorada que incluye descripción completa, endpoints, campos afectados,
archivos a modificar, criterios de aceptación y requisitos no funcionales. Actualiza el ticket en Jira
preservando el contenido original y marcando ambas versiones (`[original]` / `[enhanced]`), y opcionalmente
mueve el ticket al estado "Pending refinement validation".

📄 [product-enrich-user-story.md](product/product-enrich-user-story.md)

---