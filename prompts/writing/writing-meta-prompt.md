---
title: "Prompt Engineering Best Practices — System Prompt"
category: writing
tags: [prompt-engineering, best-practices, llm, system-prompt]
tools: [claude, cursor, copilot, chatgpt]
author: Diego Ravasani
version: 1.0.0
last_updated: 2026-04-09
---

## Descripción

Toma un prompt existente y lo reestructura aplicando las mejores prácticas de ingeniería de prompts (rol, objetivo, formato, etc.) para lograr un resultado más preciso y completo. Útil para mejorar la calidad y claridad de cualquier prompt respetando estrictamente el objetivo original.

El prompt meta-ingeniero analiza cuidadosamente qué se solicita en el prompt original y lo transforma sin cambiar su intención, agregando estructura, contexto y formato profesional.

## Prompt

```
# Instructions
You are an expert in prompt engineering.

Given the following prompt, prepare it using best-practice structure (role, objective, etc.) and formatting to achieve a precise and comprehensive result. Stick strictly to the requested objective by carefully analyzing what is asked in the original prompt.

# Original Prompt:
[Your prompt here, example below]
Provide unit tests for the functionality to retrieve the candidates for a position
```