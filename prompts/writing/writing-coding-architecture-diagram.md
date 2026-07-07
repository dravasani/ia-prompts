---
title: "Diagrama de arquitectura HTML desde múltiples proyectos"
category: coding
tags: [architecture, diagram, html, multi-repo, reverse-engineering]
tools: [claude, cursor]
author: ivan.loyarte
version: 1.0.0
last_updated: 2026-06-03
---

## Descripción

Genera un diagrama de arquitectura HTML auto-contenido a partir de un directorio con múltiples proyectos del mismo dominio. El agente escanea el stack tecnológico, conexiones entre servicios, mensajería, bases de datos y endpoints expuestos; clasifica cada proyecto en capas (Frontend, BFF, Gateway, Service, Data, Infra, External); y produce un archivo `architecture-diagram.html` con tema oscuro (Tokyo Night), swimlanes por capa y cards con conexiones cruzadas. Útil para documentar arquitecturas existentes sin intervención manual.

## Prompt

---

Estás en un directorio que contiene múltiples proyectos/repositorios del mismo dominio o scope. Tu
tarea es escanear todos profundamente y generar un diagrama de arquitectura HTML completo.

FASE 1: Exploración

Escanea todos los subdirectorios del directorio actual. Para cada proyecto, extrae:

Stack tecnológico
- Lenguaje y versión (pom.xml, build.gradle, package.json, .nvmrc, pyproject.toml, go.mod, etc.)
- Frameworks y versiones (spring-boot-starter-parent, @angular/core, etc.)
- Tipo de app (REST API, BFF, Gateway, frontend Angular/React, worker, lib, BO)

Conexiones entre servicios
- Clientes HTTP declarados: OpenFeign (@FeignClient), RestTemplate, WebClient, HttpClient, axios,
fetch, módulos Angular con HttpClient
- URLs base o service names referenciados en configs: application.yml, application.properties,
environment.ts, environment.prod.ts, .env
- Si el servicio referenciado existe como carpeta en el mismo directorio → es una conexión interna; si
no → es externa

Mensajería y eventos
- RabbitMQ: exchanges, queues, bindings (@RabbitListener, RabbitTemplate, spring.rabbitmq.*)
- Kafka: topics, producers/consumers
- Cualquier otro bus de eventos

Bases de datos
- Tipo: MongoDB, PostgreSQL, MySQL, Redis, Elasticsearch, etc.
- Conexión en configs: spring.data.mongodb.uri, spring.datasource.*, MONGO_URI, etc.
- Nombre de la base si está explícito

Flujos principales
- Endpoints expuestos: controllers, @RequestMapping, @RestController, rutas Angular, router.get/post
- Módulos internos (si el proyecto tiene módulos maven/gradle o libs angular internas)
- Patrones relevantes: SSR, cache, auth, scheduler, migration

FASE 2: Clasificación en capas

Clasifica cada proyecto en una de estas capas:

┌──────────┬─────────────────────────────────────────────────────────────┐
│   Capa   │                          Criterio                           │
├──────────┼─────────────────────────────────────────────────────────────┤
│ Frontend │ Angular, React, Vue, Next.js — app de usuario final o BO    │
├──────────┼─────────────────────────────────────────────────────────────┤
│ BFF      │ Backend que sirve exclusivamente a un frontend              │
├──────────┼─────────────────────────────────────────────────────────────┤
│ Gateway  │ Enruta tráfico entre frontend y múltiples servicios backend │
├──────────┼─────────────────────────────────────────────────────────────┤
│ Service  │ API o worker backend de negocio                             │
├──────────┼─────────────────────────────────────────────────────────────┤
│ Infra    │ Bus de mensajes, cache, scheduler, job                      │
├──────────┼─────────────────────────────────────────────────────────────┤
│ Data     │ Base de datos, store de sesión                              │
├──────────┼─────────────────────────────────────────────────────────────┤
│ External │ API de terceros o interna fuera del directorio scaneado     │
├──────────┼─────────────────────────────────────────────────────────────┤
│ User     │ Actor humano que inicia el flujo                            │
└──────────┴─────────────────────────────────────────────────────────────┘

FASE 3: Generación del diagrama HTML

Genera un único archivo HTML architecture-diagram.html con el siguiente diseño exacto. No uses
librerías externas; todo CSS y JS debe estar inline.

Diseño requerido

- Tema oscuro con paleta de colores tipo Tokyo Night:
--bg: #13141f
--bg-panel: #1a1b26
--surface: #1f2335
--surface2: #24283b
--border: #3b4261
--text: #c0caf5
--text-dim: #565f89
--text-muted: #414868
- Colores por capa (usar como accent izquierdo en cards y color del lane label):
Usuario:   #7dcfff
Frontend:  #7aa2f7
BFF:       #bb9af7
Gateway:   #ff9e64
Service:   #9ece6a
Data:      #e0af68
Infra:     #2ac3de
External:  #f7768e
- Estructura de página:
  - Header centrado con el nombre del dominio
  - Un div.diagram por cada grupo lógico identificado (si todos los proyectos forman un solo sistema,
un diagrama; si hay subsistemas claros, uno por subsistema)
  - Cada diagrama tiene un div.lanes con filas tipo swimlane
- Estructura de cada swimlane (.lane):
  - Columna izquierda fija (108px): etiqueta de la capa con su color
  - Línea vertical divisoria sutil
  - Área de cards flexible con wrap
- Estructura de cada card:
```html
<div class="card c-{tipo}">
  <div class="card-tag">{tipo/framework abreviado}</div>
  <div class="card-name">{nombre del proyecto}</div>
  <div class="card-tech">{lenguaje versión · framework versión}</div>
  <div class="card-desc">{descripción breve del rol}</div>
  <div class="card-connects">→ <span>{servicio1, servicio2}</span></div>
</div>
```
  - Borde izquierdo coloreado según capa
  - card-tag con background semitransparente del color de la capa
  - Hover: leve translateY(-2px) + box-shadow
- Conectores entre lanes (div.lane-conn): flecha vertical con label de protocolo (HTTP/HTTPS,
OpenFeign/REST, RabbitMQ events, persistencia, etc.)
- Leyenda al pie de cada diagrama con un pip coloreado por cada capa usada

Requisitos adicionales

- Los proyectos que se conectan entre sí dentro del directorio deben tener la referencia cruzada en
card-connects
- Las conexiones a sistemas fuera del directorio van en la capa External con una card por cada sistema
externo distinto
- Si un mismo proyecto pertenece a múltiples diagramas (shared lib), mostrarlo en ambos con una nota
(shared)
- El HTML debe ser auto-contenido y abrirse directamente en el browser sin servidor

Entregable

Un único archivo architecture-diagram.html listo para abrir. Antes de generarlo, muestra un resumen en
texto de lo que encontraste:
- Lista de proyectos por capa
- Conexiones internas identificadas
- Sistemas externos referenciados
- Bases de datos y buses de mensajes

Luego procede a generar el HTML completo.
