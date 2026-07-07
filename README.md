Thu Jun 11 2026 # 🤖 ai-prompts

Repositorio centralizado de prompts optimizados para herramientas de agentes de IA. El objetivo es que el equipo técnico y de producto pueda **reusar, mejorar y contribuir** prompts de forma ordenada, versionada y colaborativa.

---

## ¿Por qué este repositorio?

- Evitar que los buenos prompts queden en silos individuales o se pierdan.
- Tener una base compartida que mejore con el tiempo gracias a las contribuciones del equipo.
- Facilitar la adopción de IA en distintos flujos de trabajo sin empezar desde cero.

---

## Estructura de directorios propuesta

```
ai-prompts/
├── docs/                     # Informacion util y de referencia sobre mejores practicas de prompt
├── prompts/                  # Prompts listos para usar, organizados por dominio
│   ├── coding/               # Revisión de código, generación, debugging, tests
│   ├── writing/              # Redacción técnica, posts, documentación, emails
│   ├── analysis/             # Análisis de datos, métricas, síntesis de información
│   ├── product/              # Research, user stories, PRDs, feedback
│   ├── qa/                   # Testing exploratorio, casos de prueba, regresión
│   └── ops/                  # Runbooks, postmortems, alertas, automatizaciones
│
├── README.md
```

---

## Convención de nombre de archivos

Cada prompt es un archivo Markdown con el siguiente formato:

```
{categoria}-{nombre-descriptivo}.md
```

Ejemplos:
- `coding-review-pull-request.md`
- `writing-technical-post.md`
- `analysis-metrics-summary.md`

---

## Estructura de un prompt

Cada archivo `.md` debe seguir esta estructura:

```markdown
---
title: "Revisión de Pull Request"
category: coding
tags: [code-review, best-practices, git]
tools: [claude, cursor, copilot]
author: nombre.apellido
version: 1.0.0
last_updated: 2025-04-08
---

## Descripción

Breve descripción de para qué sirve este prompt y en qué contexto usarlo.

## Prompt

---

## Cómo contribuir

1. Clonar el repositorio y crear una branch: `git checkout -b prompt/nombre-del-prompt`
2. Agregar el archivo en la carpeta correspondiente siguiendo la convención de nombres.
3. Abrir un Pull Request.
4. Al menos un review de otro miembro del equipo antes de mergear.

Antes de abrir un PR, revisá si ya existe un prompt similar para evitar duplicados o bien proponer una mejora sobre el existente.

---

## Guías de escritura de prompts

Algunas buenas prácticas que seguimos en este repo:

- **Sé específico en el rol**: indicar al modelo qué rol debe asumir mejora la consistencia de los resultados.
- **Definí el formato de salida**: si necesitás JSON, Markdown o texto plano, especificalo explícitamente.
- **Usá variables con doble llave**: `{{variable}}` para hacer los prompts reutilizables y fácilmente parametrizables.
- **Incluí ejemplos cuando puedas**: los prompts con ejemplos (few-shot) generalmente producen mejores resultados.
- **Indicá restricciones**: decile al modelo qué **no** debe hacer es tan importante como decirle qué hacer.
- **Probá en al menos dos herramientas** antes de hacer merge: lo que funciona en Claude puede no comportarse igual en otro modelo.

---

## Stack de herramientas soportadas

Este repositorio está pensado para ser agnóstico de herramienta. Los prompts funcionan con:

- Claude (claude.ai, API, Claude Code)
- Cursor / GitHub Copilot
- ChatGPT / OpenAI API
- Agentes custom (LangChain, CrewAI, AutoGen, etc.)
- Cualquier interfaz que acepte prompts de texto

---

## Licencia

Uso interno. Todos los derechos reservados.