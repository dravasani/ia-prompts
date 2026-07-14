---
title: "User Story Enricher"
category: product
tags: [product, user-stories, refinement, backlog, enrichment]
tools: [claude, cursor]
author: Diego Ravasani
version: 2.0.0
last_updated: 2026-07-14
---

## Descripción

Analiza una historia de usuario y determina si cuenta con el nivel de detalle técnico y funcional necesario para que un desarrollador la complete de forma autónoma. Si detecta deficiencias, genera una versión mejorada que incluye descripción completa, endpoints, campos afectados, archivos a modificar, criterios de aceptación y requisitos no funcionales.

La historia de usuario puede pasarse de tres formas distintas como `$ARGUMENTS`:
- **Texto plano**: el contenido de la historia pegado directamente en el prompt.
- **Ruta a un archivo**: por ejemplo `docs/historias/HU-102.md`.
- **Link**: una URL donde esté documentada (Jira, Confluence, Notion, un gist, etc.).

El resultado se devuelve en markdown, preservando el contenido original y marcando ambas versiones (`[original]` / `[enhanced]`), sin asumir ninguna herramienta de gestión en particular.

**Nota:** Este prompt requiere acceso al contexto técnico del proyecto (@documentation). Si la historia se referencia por link y la herramienta no tiene acceso a la web o al sistema donde vive ese link, pedirá al usuario que pegue el contenido como texto.

## Prompt

```
Please analyze and enrich the following user story: $ARGUMENTS.

Follow these steps:

1. Determine how the user story was provided:
   - If it looks like plain text, use it directly as the user story content.
   - If it looks like a file path, read that file to get the user story content.
   - If it looks like a URL/link, try to fetch its content. If you cannot access it (no network/tool access), ask the user to paste the user story as plain text instead.
2. You will act as a product expert with technical knowledge
3. Understand the problem described in the user story
4. Decide whether or not the User Story is completely detailed according to product's best practices: Include a full description of the functionality, a comprehensive list of fields to be updated, the structure and URLs of the necessary endpoints, the files to be modified according to the architecture and best practices, the steps required for the task to be considered complete, how to update any relevant documentation or create unit tests, and non-functional requirements related to security, performance, etc
5. If the user story lacks the technical and specific detail necessary to allow the developer to be fully autonomous when completing it, provide an improved story that is clearer, more specific, and more concise in line with product best practices described in step 4. Use the technical context you will find in 
@documentation. Return it in markdown format.
6. Present the result in markdown, adding the new content after the old one and marking each section with the h2 headings [original] and [enhanced]. Apply proper formatting to make it readable and visually clear, using appropriate text types (lists, code snippets...).
7. If the user story was read from a file, ask the user whether they want the enriched version saved back to that file (or to a new one) before writing anything to disk.
```