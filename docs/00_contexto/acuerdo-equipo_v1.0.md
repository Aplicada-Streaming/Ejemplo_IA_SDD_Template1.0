# Acuerdo de Equipo (Team Charter / Working Agreements)

**Proyecto:** Motor DSL de Generación de Documentos
**Documento:** acuerdo-equipo_v1.0.md
**Versión:** 1.0
**Estado:** Borrador
**Fecha:** 2026-03-28
**Autor:** Equipo Técnico

---

# 1. Propósito

Establecer los acuerdos de trabajo, roles y compromisos del equipo. Este documento sirve como referencia compartida para las normas y prácticas que el equipo se compromete a seguir.

---

# 2. Equipo y Roles Scrum

| Rol | Persona | Notas |
| --- | ------- | ----- |
| Product Owner | [Pendiente de asignar] | Responsable del backlog y priorización |
| Scrum Master | [Pendiente de asignar] | Facilitador del proceso Scrum |
| Equipo de Desarrollo | [Pendiente de completar] | Listar nombres y especialización |

### Miembros del equipo de desarrollo

| Nombre | Especialización | Notas |
| ------ | --------------- | ----- |
| [Nombre 1] | [Área de expertise] | - |
| [Nombre 2] | [Área de expertise] | - |
| [Nombre 3] | [Área de expertise] | - |

---

# 3. Cadencia de Ceremonias

| Ceremonia | Cuándo | Duración | Notas |
| --------- | ------ | -------- | ----- |
| Sprint Planning | Día 1 de cada sprint | 2 horas | Todo el equipo Scrum |
| Daily Scrum | Diario | 15 minutos | Formato async o sincrónico [definir] |
| Sprint Review | Último día del sprint | 1 hora | Demo a stakeholders |
| Sprint Retrospective | Después del Review | 1 hora | Solo el equipo Scrum |
| Backlog Refinement | Semanal, mitad del sprint | 1 hora | Preparación de ítems futuros |

---

# 4. Acuerdos de Trabajo

## 4.1 Branching Strategy

- **Modelo:** GitFlow
- **Branches principales:** `main` (producción), `develop` (integración)
- **Branches de trabajo:** `feature/*`, `bugfix/*`, `hotfix/*`
- **Convención de nombres:** `feature/US-XX-descripcion-corta`

## 4.2 Code Review

- Mínimo **1 aprobación** antes de merge a `develop`.
- Las revisiones se realizan en un máximo de 24 horas hábiles.
- El autor del PR es responsable de resolver los comentarios.

## 4.3 Comunicación

- **Canal principal:** [Canal Slack/Teams — pendiente de definir]
- **Bloqueos:** Comunicar inmediatamente al equipo, no esperar al Daily.
- **Decisiones técnicas:** Documentar en ADRs cuando sean significativas.

## 4.4 Horario Core

- **Horario core:** [Pendiente de definir]
- Durante el horario core, todos los miembros están disponibles para consultas.

## 4.5 Documentación

- Todo cambio relevante se refleja en `docs/`.
- La documentación se actualiza como parte del Definition of Done.

---

# 5. Definition of Done

Ver [definition-of-done_v1.0.md](../08_calidad_y_pruebas/definition-of-done_v1.0.md)

---

# 6. Definition of Ready

Ver [definition-of-ready_v1.0.md](../06_backlog-tecnico/definition-of-ready_v1.0.md)

---

# 7. Herramientas

| Categoría | Herramienta | Notas |
| --------- | ----------- | ----- |
| IDE | Visual Studio / VS Code | Según preferencia del desarrollador |
| Repositorio | Git | Hosted en GitHub |
| CI/CD | GitHub Actions | Pipelines de build, test y deploy |
| Tracking | [Pendiente de definir] | GitHub Projects, Jira u otra |
| Comunicación | [Pendiente de definir] | Slack, Teams u otra |

---

# 8. Control de Cambios

| Versión | Fecha      | Descripción     |
| ------- | ---------- | --------------- |
| 1.0     | 2026-03-28 | Versión inicial |

---

**Fin del documento**
