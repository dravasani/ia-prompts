---
name: git-commit-conventions
description: Use this skill whenever creating git commits, staging changes for commit, writing commit messages, cleaning up commit history (rebase/squash), or opening a PR in this repository. Ensures every commit follows Conventional Commits format, atomic scope, imperative mood, and proper documentation of intent. Trigger this proactively any time you are about to run `git commit`, `git commit --amend`, or `git rebase -i` — do not wait for the user to explicitly ask about commit style.
---

# Git Commit Conventions

Reglas obligatorias para escribir y organizar commits en este repositorio. Aplicá esto SIEMPRE que vayas a ejecutar `git commit`, sin que el usuario lo tenga que pedir explícitamente.

## 1. Formato del mensaje

```
<tipo>(<scope opcional>): <resumen corto en modo imperativo>

<cuerpo opcional: explica el "por qué", no el "qué">

<footer opcional: referencias a issues, breaking changes>
```

- **Resumen:** máximo ~72 caracteres, modo imperativo, sin punto final.
- **Línea en blanco obligatoria** entre resumen y cuerpo.
- **Cuerpo:** solo si el "por qué" no es obvio a partir del diff. No repetir lo que el diff ya muestra línea por línea.

## 2. Tipos válidos (Conventional Commits)

| Tipo | Uso |
|---|---|
| `feat` | Nueva funcionalidad |
| `fix` | Corrección de bug |
| `docs` | Solo documentación |
| `style` | Formato, espacios, sin cambio de lógica |
| `refactor` | Cambio de código sin arreglar bug ni agregar feature |
| `test` | Agregar o corregir tests |
| `chore` | Mantenimiento (deps, configs, build) |
| `perf` | Mejora de performance |
| `ci` | Cambios en pipelines/CI |

Si el cambio no encaja claramente en ninguno, preguntar al usuario antes de elegir uno por defecto.

## 3. Modo imperativo — regla no negociable

El resumen debe completar: *"Si se aplica, este commit va a **___**"*.

```
✅ fix(auth): corregir expiración de tokens JWT
✅ feat(pedidos): agregar endpoint de cancelación
❌ fixed bug in tokens          → pasado
❌ agregando endpoint de...     → gerundio
❌ arreglos varios              → no dice qué
```

## 4. Commits atómicos

Un commit = un cambio lógico. Antes de comitear, revisar el diff con `git diff --staged` y preguntarse: *¿esto son dos cambios sin relación mezclados?* Si es así, separar en commits distintos usando `git add -p` para stagear por partes, en vez de un solo commit gigante.

No mezclar en un mismo commit, por ejemplo: un fix + una nueva feature + un refactor sin relación. Cada uno va aparte.

## 5. Breaking changes

Si el cambio rompe compatibilidad hacia atrás (API, contrato de datos, firma pública):

```
feat(api)!: cambiar formato de respuesta de /pedidos a paginado

BREAKING CHANGE: la respuesta ya no es un array directo, ahora es
un objeto { data: [...], page: 1, totalPages: 5 }. Clientes deben
actualizar su parsing.
```

Usar `!` después del tipo/scope Y el footer `BREAKING CHANGE:` — ambos, no uno solo.

## 6. Referencias a issues

Si el usuario menciona un número de ticket/issue (Jira, GitHub Issues, etc.), incluirlo en el footer:

```
Closes #1204
Refs JIRA-4521
```

Si no se menciona ningún ticket, no inventar uno ni preguntar por uno a menos que el repo tenga convención de requerirlo (revisar CONTRIBUTING.md si existe).

## 7. Antes de cada commit — checklist obligatorio

Antes de ejecutar `git commit`, verificar:

- [ ] ¿El resumen está en modo imperativo?
- [ ] ¿El tipo elegido es correcto?
- [ ] ¿Representa un único cambio lógico (no mezclar features/fixes sin relación)?
- [ ] ¿El cuerpo (si existe) explica el *por qué*, no repite el diff?
- [ ] ¿Hay algún ticket/issue mencionado por el usuario que deba referenciarse?
- [ ] ¿Es un breaking change? Si sí, ¿está marcado con `!` y `BREAKING CHANGE:`?

Si algo de esto no está claro a partir del contexto de la conversación o del diff, preguntar al usuario antes de comitear en vez de asumir.

## 8. Limpieza de historia antes de abrir un PR

Si el usuario pide "limpiar" o "prolijar" el historial antes de un PR, usar `git rebase -i` con:
- `squash` para combinar commits de "wip"/fixes menores dentro del commit relevante.
- `reword` para corregir mensajes que no sigan estas convenciones.
- Nunca hacer esto sobre commits que ya fueron pusheados a una rama compartida donde otros puedan tener ese historial — confirmar con el usuario antes.

## 9. Ejemplos de referencia rápida

```
feat(pagos): agregar soporte para pagos con transferencia bancaria
fix(inventario): evitar stock negativo en operaciones concurrentes
refactor(pedidos): extraer lógica de validación a PedidoValidator
chore(deps): actualizar Spring Boot a 3.2.5
test(pedidos): agregar cobertura para cancelación con reembolso parcial
docs(readme): documentar variables de entorno requeridas
```

## 10. Qué NO hacer nunca

- No commitear con mensajes tipo `"wip"`, `"fix"`, `"asdasd"`, `"cambios"`.
- No usar `git commit -m` con un mensaje genérico cuando el cambio amerita un cuerpo explicativo.
- No mezclar cambios de formato/estilo (`style`) con cambios de lógica (`feat`/`fix`) en el mismo commit — el ruido dificulta el code review.
- No hacer `git push --force` sobre ramas compartidas para "limpiar" historia sin confirmación explícita del usuario.
