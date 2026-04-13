# Metodologías Ágiles y Gestión de Tareas con Jira

**Documento:** metodologias-agiles-jira_v1.0.md  
**Versión:** 1.0  
**Fecha:** 2026-04-13  
**Autor:** Equipo de Desarrollo  
**Estado:** Activo  
**Contexto:** Guía de referencia para gestión ágil de proyectos de software

---

## PARTE 1 — METODOLOGÍAS ÁGILES

---

### Sección 1 — Propósito del documento

#### 1.1 Para qué sirve este documento

Este documento es una guía integral de referencia sobre metodologías ágiles y gestión de tareas con Jira. Consolida los conceptos fundamentales de Scrum, Kanban, XP y frameworks de escala, junto con la operativa práctica de Jira como herramienta de tracking.

El objetivo es que un desarrollador o estudiante pueda consultar este documento como fuente única para entender:

- Qué son las metodologías ágiles y por qué existen
- Cómo funcionan Scrum y Kanban en la práctica
- Cómo se estructuran user stories, épicas y tareas técnicas
- Cómo se gestiona un proyecto ágil en Jira
- Cómo se relaciona todo esto con la documentación SDD del proyecto

#### 1.2 A quién está dirigido

- Desarrolladores que se incorporan a equipos ágiles por primera vez
- Estudiantes de ingeniería de software que necesitan una referencia práctica
- Miembros de equipo que necesitan entender la gestión de proyectos más allá del código

#### 1.3 Relación con la documentación SDD del proyecto

Este proyecto sigue el enfoque **Specification-Driven Development (SDD)**, donde la documentación guía el desarrollo a través de una cadena de trazabilidad:

```
Visión del Producto          →  docs/00_contexto/vision-producto_v1.0.md
    ↓
Necesidades de Negocio       →  docs/01_necesidades_negocio/necesidades-negocio_v1.0.md
    ↓
Especificación Funcional     →  docs/02_especificacion_funcional/especificacion-funcional_v1.0.md
    ↓
Arquitectura Técnica         →  docs/05_arquitectura_tecnica/arquitectura-solucion_v1.0.md
    ↓
Product Backlog (US)         →  docs/06_backlog-tecnico/product-backlog_v1.0.md
    ↓
Backlog Técnico (BT)         →  docs/06_backlog-tecnico/backlog-tecnico_v1.0.md
    ↓
Plan de Sprint               →  docs/07_plan-sprint/plan-iteracion_sprint-XX_v1.0.md
    ↓
Testing y Calidad            →  docs/08_calidad_y_pruebas/definition-of-done_v1.0.md
    ↓
DevOps y Deploy              →  docs/09_devops/
```

Cada nivel de esta cadena alimenta al siguiente. Las metodologías ágiles (este documento) gobiernan **cómo** se ejecuta el trabajo desde el Product Backlog hacia abajo: cómo se priorizan las historias, cómo se planifican los sprints, cómo se mide el progreso y cómo se mejora continuamente.

---

### Sección 2 — Manifiesto Ágil y principios fundamentales

#### 2.1 Los 4 valores del Manifiesto Ágil

El [Manifiesto Ágil](https://agilemanifesto.org/) fue firmado en 2001 por 17 profesionales del software. Establece 4 valores:

| # | Valoramos más... | ...sobre... |
|---|---|---|
| 1 | **Individuos e interacciones** | Procesos y herramientas |
| 2 | **Software funcionando** | Documentación exhaustiva |
| 3 | **Colaboración con el cliente** | Negociación contractual |
| 4 | **Respuesta ante el cambio** | Seguir un plan |

> **Nota importante:** "Valoramos más" no significa que los elementos de la derecha no importen. Significa que, ante un conflicto, priorizamos los de la izquierda. En el proyecto Motor DSL, por ejemplo, tenemos documentación extensa (SDD), pero siempre al servicio del software funcionando — la documentación guía la construcción, no la reemplaza.

#### 2.2 Los 12 principios ágiles

| # | Principio | Explicación práctica |
|---|---|---|
| 1 | Satisfacer al cliente mediante entrega temprana y continua de software con valor | No esperar 6 meses para entregar. Entregar incrementos cada sprint. |
| 2 | Aceptar cambios en los requisitos, incluso tarde en el desarrollo | Los cambios son oportunidades, no amenazas. El backlog es dinámico. |
| 3 | Entregar software funcionando frecuentemente (semanas, no meses) | Sprints de 1-4 semanas. Cada sprint produce un incremento usable. |
| 4 | Negocio y desarrolladores deben trabajar juntos diariamente | El Product Owner no desaparece entre sprints. Está disponible. |
| 5 | Construir proyectos en torno a individuos motivados | Dar autonomía al equipo. Confiar en sus decisiones técnicas. |
| 6 | La comunicación cara a cara es la más eficiente | Dailys, reviews, retros. No reemplazar todo con emails y tickets. |
| 7 | El software funcionando es la medida principal de progreso | No medir progreso por documentos escritos sino por features entregadas. |
| 8 | Desarrollo sostenible: mantener un ritmo constante indefinidamente | No hacer crunches. Si el equipo hace 18 SP por sprint, no comprometer 30. |
| 9 | Atención continua a la excelencia técnica y buen diseño | Refactoring, testing, code reviews. La deuda técnica se gestiona, no se ignora. |
| 10 | Simplicidad: maximizar el trabajo no realizado | YAGNI (You Aren't Gonna Need It). No construir features "por si acaso". |
| 11 | Las mejores arquitecturas emergen de equipos auto-organizados | El equipo decide cómo implementar, no un arquitecto aislado. |
| 12 | Reflexión regular sobre cómo ser más efectivo | Las retrospectivas no son opcionales. El proceso mejora sprint a sprint. |

#### 2.3 Contexto histórico: por qué surgió

Antes del manifiesto ágil, el modelo dominante era **Waterfall** (cascada), popularizado por Winston Royce en 1970. En cascada, el proyecto avanza en fases secuenciales rígidas: Requisitos → Diseño → Implementación → Verificación → Mantenimiento. Cada fase debe completarse antes de iniciar la siguiente.

Los problemas de waterfall en software:

- El cliente no ve el producto hasta el final (meses o años después)
- Los cambios de requisitos son costosos y resisten
- Los bugs se descubren tarde, cuando corregirlos es caro
- El equipo no recibe feedback hasta que es demasiado tarde

El manifiesto ágil surgió como respuesta a estos problemas, proponiendo un enfoque iterativo e incremental.

#### 2.4 Tabla comparativa: Waterfall vs. Ágil

| Aspecto | Waterfall | Ágil |
|---|---|---|
| **Planificación** | Completa y detallada al inicio (Big Design Up Front) | Progresiva: planificación detallada solo para el sprint actual |
| **Entrega** | Una sola entrega al final del proyecto | Entregas incrementales cada 1-4 semanas |
| **Feedback** | Al final, cuando el producto está "terminado" | Continuo: cada sprint review genera feedback |
| **Gestión de cambios** | Resistidos; requieren proceso formal de change request | Bienvenidos; el backlog se reprioriza continuamente |
| **Documentación** | Exhaustiva y previa al código | Suficiente y al servicio del desarrollo (como en SDD) |
| **Riesgo** | Concentrado al final (integración y testing tardío) | Distribuido: cada sprint integra, prueba y entrega |
| **Roles** | Rígidos y jerárquicos (Project Manager decide todo) | Colaborativos y auto-organizados (PO, SM, Dev Team) |
| **Testing** | Fase separada al final | Continuo durante todo el desarrollo (TDD, CI) |
| **Éxito se mide por** | Cumplimiento del plan original | Valor entregado al cliente |

---

### Sección 3 — Scrum

#### 3.1 Definición y origen

**Scrum** es un framework ágil para desarrollar, entregar y mantener productos complejos. Fue formalizado por Ken Schwaber y Jeff Sutherland, y su referencia canónica es la [Scrum Guide 2020](https://scrumguides.org/).

Scrum no es una metodología prescriptiva — es un framework ligero que define roles, eventos y artefactos mínimos. El equipo decide cómo trabajar dentro de ese marco.

#### 3.2 Los 3 pilares

| Pilar | Definición | Ejemplo práctico |
|---|---|---|
| **Transparencia** | El proceso y el trabajo deben ser visibles para todos | El board de Jira está visible. La velocity se registra en `velocidad-equipo_v1.0.md`. Todos ven el estado real. |
| **Inspección** | Los artefactos y el progreso se inspeccionan frecuentemente | Cada daily se revisa el board. Cada review se inspecciona el incremento. Cada retro se inspecciona el proceso. |
| **Adaptación** | Cuando algo se desvía, se ajusta lo antes posible | Si en la daily se detecta un bloqueo, se actúa hoy, no al final del sprint. Si la velocity baja, se reduce el compromiso del próximo sprint. |

#### 3.3 Los 5 valores

| Valor | Significado | Anti-ejemplo |
|---|---|---|
| **Compromiso** | El equipo se compromete con los objetivos del sprint | No comprometerse a 40 SP cuando la velocity es 18 |
| **Coraje** | Tener la valentía de hacer lo correcto y trabajar en problemas difíciles | Decir "esta historia no cumple el DoR" aunque el PO presione |
| **Foco** | Concentrarse en el trabajo del sprint y los objetivos del equipo | No meter historias al sprint a mitad de camino sin justificación |
| **Apertura** | Ser transparente sobre el trabajo y los desafíos | Reportar impedimentos en la daily, no ocultarlos |
| **Respeto** | Respetar que cada persona es capaz y actúa con buena intención | No culpar al compañero si un spike no dio el resultado esperado |

#### 3.4 Roles

##### Tabla comparativa de roles

| Aspecto | Product Owner | Scrum Master | Development Team |
|---|---|---|---|
| **Responsabilidad** | Maximizar el valor del producto | Facilitar el proceso Scrum | Construir el incremento |
| **Gestiona** | Product Backlog, priorización | Impedimentos, ceremonias | Trabajo técnico del sprint |
| **Decide** | Qué se construye y en qué orden | Cómo se facilita el proceso | Cómo se implementa técnicamente |
| **NO hace** | No decide el cómo técnico | No asigna tareas ni gestiona personas | No decide prioridad de negocio |
| **Reporta a** | Stakeholders / Negocio | Nadie (es un líder servicial) | Se auto-organiza |
| **Anti-patrón** | PO ausente o proxy sin poder de decisión | SM que asigna tareas como Project Manager | Equipo que espera que le digan qué hacer |

##### Product Owner (PO)

**Responsabilidades:**
- Gestionar y priorizar el Product Backlog
- Definir los criterios de aceptación de cada historia
- Tomar decisiones de negocio sobre qué se construye
- Aceptar o rechazar el incremento en la Sprint Review
- Maximizar el valor del trabajo del equipo

**Qué NO hace:**
- No decide la arquitectura ni las decisiones técnicas
- No asigna tareas a personas específicas
- No cambia el scope del sprint a mitad de camino (sin negociación)

**Anti-patrones comunes:**
- *El PO proxy:* alguien que "representa" al PO pero no tiene poder de decisión real
- *El PO ausente:* aparece solo en el planning y desaparece hasta la review
- *El PO micromanager:* decide el cómo técnico además del qué

##### Scrum Master (SM)

**Responsabilidades:**
- Facilitar las ceremonias Scrum
- Remover impedimentos del equipo
- Proteger al equipo de interrupciones externas
- Coaching en prácticas ágiles
- Asegurar que se respeten los acuerdos (DoR, DoD, WIP limits)

**Qué NO hace:**
- No es un Project Manager — no asigna tareas ni controla horarios
- No es el jefe del equipo — es un líder servicial
- No decide qué se construye — eso es responsabilidad del PO

**Anti-patrones comunes:**
- *El SM secretario:* solo agenda reuniones y toma notas
- *El SM policía:* controla y vigila en vez de facilitar
- *El SM ausente:* no remueve impedimentos activamente

##### Development Team

**Responsabilidades:**
- Auto-organizarse para entregar el incremento
- Estimar las historias de usuario
- Descomponer historias en tareas técnicas
- Cumplir el Definition of Done
- Participar activamente en todas las ceremonias

**Qué NO hace:**
- No decide la prioridad del backlog — eso lo hace el PO
- No reporta a un líder técnico — se auto-organiza
- No trabaja en historias fuera del sprint sin acordarlo

**Anti-patrones comunes:**
- *El equipo silencioso:* no habla en las dailies ni en las retros
- *El héroe solitario:* una persona hace todo, el resto espera
- *El equipo fragmentado:* cada uno trabaja en silos sin comunicarse

#### 3.5 Artefactos

##### Product Backlog

**Definición:** Lista priorizada de todo lo que se necesita en el producto. Es el único origen de requisitos para el trabajo del equipo.

**Quién lo gestiona:** El Product Owner, con input del equipo y stakeholders.

**En este proyecto:**  
El Product Backlog está documentado en `../docs/06_backlog-tecnico/product-backlog_v1.0.md` con 31 User Stories clasificadas por prioridad MoSCoW:

| Prioridad | Descripción | Ejemplo del proyecto |
|---|---|---|
| Must Have | Imprescindible para el MVP | US-03: Parser DSL básico, US-09: Renderizar ESC/POS |
| Should Have | Importante pero no bloqueante | US-10: Renderizar texto plano, US-16: Adaptar al perfil del dispositivo |
| Could Have | Deseable si hay capacidad | US-27: Renderizar a PDF |
| Won't Have (v1.0) | Fuera de alcance para esta versión | Editor visual, scripting avanzado |

##### Sprint Backlog

**Definición:** Subconjunto del Product Backlog que el equipo se compromete a entregar durante el sprint actual, más el Sprint Goal y el plan para lograrlo.

**Quién lo gestiona:** El Development Team.

**En este proyecto:**  
Cada sprint tiene su plan documentado en `../docs/07_plan-sprint/plan-iteracion_sprint-XX_v1.0.md`. Por ejemplo, el Sprint 01 compromete US-01 a US-04 con un total de 48 SP y el objetivo: *"Implementar el MVP técnico del núcleo del motor, permitiendo crear la estructura base, definir el AST e implementar el parser DSL básico."*

##### Incremento

**Definición:** La suma de todos los ítems del Product Backlog completados durante el sprint, más los incrementos de sprints anteriores. Cada incremento debe ser usable y cumplir el Definition of Done.

**Quién lo valida:** El Product Owner durante el Sprint Review.

**En este proyecto:**
- El Definition of Ready está en `../docs/06_backlog-tecnico/definition-of-ready_v1.0.md`
- El Definition of Done está en `../docs/08_calidad_y_pruebas/definition-of-done_v1.0.md`

El DoD incluye criterios de código (compila, sin warnings, PR aprobado), testing (unitarios, integración, cobertura ≥ 70%, CI verde), calidad (SLAs de performance) y documentación.

#### 3.6 Eventos / Ceremonias

| Evento | Propósito | Timebox | Participantes | Entradas | Salidas |
|---|---|---|---|---|---|
| **Sprint Planning** | Planificar qué se va a construir en el sprint y cómo | 2-4 horas (sprint de 2 semanas) | PO, SM, Dev Team | Product Backlog priorizado, velocity histórica, DoR | Sprint Backlog, Sprint Goal |
| **Daily Scrum** | Sincronizar al equipo y detectar impedimentos | 15 minutos | Dev Team (SM facilita) | Estado del sprint board | Impedimentos identificados, plan del día |
| **Sprint Review** | Inspeccionar el incremento y obtener feedback | 1-2 horas | PO, SM, Dev Team, Stakeholders | Incremento completado | Feedback, ajustes al backlog |
| **Sprint Retrospective** | Reflexionar sobre el proceso y definir mejoras | 1-1.5 horas | SM, Dev Team (PO opcional) | Observaciones del sprint | Acciones de mejora con responsable |
| **Refinamiento (Grooming)** | Detallar, estimar y descomponer historias futuras | 1-2 horas (no es evento formal de Scrum) | PO, Dev Team, SM | Historias candidatas del backlog | Historias refinadas con DoR cumplido |

**Templates del proyecto para ceremonias:**
- Sprint Review → `../docs/07_plan-sprint/template-sprint-review_v1.0.md`
- Sprint Retrospectiva → `../docs/07_plan-sprint/template-sprint-retrospectiva_v1.0.md`

#### 3.7 El Sprint

**Definición:** Un período fijo de tiempo (timebox) durante el cual se crea un incremento de producto "Done", usable y potencialmente entregable.

**Duración típica:** 1 a 4 semanas. En este proyecto se usan sprints de **2 semanas**.

**Qué pasa durante un sprint:**

1. **Sprint Planning** (día 1): Se define el Sprint Goal, se seleccionan historias del backlog y se descomponen en tareas
2. **Desarrollo diario** (días 1-10): El equipo trabaja en las historias. Cada día hay una Daily Scrum de 15 minutos
3. **Refinamiento** (durante el sprint): Se detallan historias para el próximo sprint
4. **Sprint Review** (último día): Se demuestra el incremento al PO y stakeholders
5. **Sprint Retrospective** (después de la review): El equipo reflexiona sobre el proceso

**Reglas del sprint:**
- El Sprint Goal no cambia a mitad del sprint
- No se agregan historias al sprint sin negociación (el PO puede negociar cambio de scope)
- Si el Sprint Goal se vuelve obsoleto, el PO puede cancelar el sprint (caso extremo)
- La calidad no se reduce — el DoD se respeta siempre

#### 3.8 Diagrama del ciclo Scrum

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          CICLO SCRUM                                    │
│                                                                         │
│   ┌──────────────┐                                                      │
│   │   PRODUCT     │◄──── Repriorización continua                        │
│   │   BACKLOG     │      (basada en feedback                            │
│   │               │       de Reviews y Retros)                          │
│   │  ┌─────────┐  │                                                     │
│   │  │ US-01   │  │    ┌──────────────────────────────────────────┐     │
│   │  │ US-02   │──┼───►│         SPRINT (2 semanas)                │     │
│   │  │ US-03   │  │    │                                          │     │
│   │  │ US-04   │  │    │  Sprint    Daily     Desarrollo          │     │
│   │  │ ...     │  │    │  Planning  Scrum     continuo            │     │
│   │  └─────────┘  │    │  (Día 1)  (15 min)  (Días 1-10)         │     │
│   └──────────────┘    │     │        │            │               │     │
│                        │     ▼        ▼            ▼               │     │
│                        │  ┌─────────────────────────────┐         │     │
│                        │  │    Sprint     Sprint Goal    │         │     │
│                        │  │    Backlog    + Tareas       │         │     │
│                        │  └─────────────────────────────┘         │     │
│                        │                    │                      │     │
│                        │                    ▼                      │     │
│                        │           ┌──────────────┐               │     │
│                        │           │ INCREMENTO   │               │     │
│                        │           │ (Done, usable │               │     │
│                        │           │  y entregable)│               │     │
│                        │           └──────┬───────┘               │     │
│                        └─────────────────┼────────────────────────┘     │
│                                          │                              │
│                                          ▼                              │
│                        ┌──────────────────────────────────┐             │
│                        │  Sprint Review                    │             │
│                        │  → Demo al PO y Stakeholders      │             │
│                        │  → Feedback sobre el incremento   │             │
│                        └──────────────┬───────────────────┘             │
│                                       │                                 │
│                                       ▼                                 │
│                        ┌──────────────────────────────────┐             │
│                        │  Sprint Retrospective             │             │
│                        │  → ¿Qué salió bien?               │             │
│                        │  → ¿Qué salió mal?                │             │
│                        │  → Acciones de mejora              │             │
│                        └──────────────────────────────────┘             │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

### Sección 4 — Kanban

#### 4.1 Definición y origen

**Kanban** (看板, "tablero visual" en japonés) es un método de gestión del flujo de trabajo que se originó en el sistema de producción de Toyota en la década de 1940. Fue adaptado al desarrollo de software por David J. Anderson en 2007.

A diferencia de Scrum, Kanban no tiene sprints, roles obligatorios ni ceremonias fijas. Se enfoca en **visualizar el flujo de trabajo** y **optimizarlo continuamente**.

#### 4.2 Principios de Kanban

| # | Principio | Explicación |
|---|---|---|
| 1 | **Visualizar el trabajo** | Todo el trabajo en progreso debe ser visible en un tablero. Si no está en el board, no existe. |
| 2 | **Limitar el Work In Progress (WIP)** | Definir límites máximos de ítems por columna. Menos WIP = más foco = menos context switching. |
| 3 | **Gestionar el flujo** | Observar y optimizar cómo fluyen los ítems a través del tablero. Detectar cuellos de botella. |
| 4 | **Hacer políticas explícitas** | Documentar las reglas: qué significa cada columna, cuándo se mueve un ítem, quién puede hacerlo. |
| 5 | **Implementar feedback loops** | Reuniones regulares para inspeccionar el sistema (standups, service delivery reviews). |
| 6 | **Mejorar colaborativamente, evolucionar experimentalmente** | Cambios incrementales basados en datos, no revoluciones. |

#### 4.3 Tablero Kanban

Un tablero Kanban típico con WIP limits:

```
┌──────────────┬──────────────┬──────────────┬──────────────┬──────────────┐
│   BACKLOG    │ IN PROGRESS  │  IN REVIEW   │     QA       │    DONE      │
│   (sin WIP)  │   WIP: 3     │   WIP: 2     │   WIP: 2     │  (sin WIP)   │
├──────────────┼──────────────┼──────────────┼──────────────┼──────────────┤
│  ┌────────┐  │  ┌────────┐  │  ┌────────┐  │  ┌────────┐  │  ┌────────┐  │
│  │ Item 7 │  │  │ Item 4 │  │  │ Item 2 │  │  │ Item 1 │  │  │ Item A │  │
│  ├────────┤  │  ├────────┤  │  └────────┘  │  └────────┘  │  ├────────┤  │
│  │ Item 8 │  │  │ Item 5 │  │              │              │  │ Item B │  │
│  ├────────┤  │  ├────────┤  │              │              │  ├────────┤  │
│  │ Item 9 │  │  │ Item 6 │  │              │              │  │ Item C │  │
│  ├────────┤  │  └────────┘  │              │              │  └────────┘  │
│  │ Item 10│  │              │              │              │              │
│  └────────┘  │              │              │              │              │
└──────────────┴──────────────┴──────────────┴──────────────┴──────────────┘
```

**Políticas de columna (ejemplo):**
- **Backlog:** Cualquier ítem priorizado por el PO o líder técnico
- **In Progress:** El desarrollador se asigna el ítem. Máximo 1 ítem por persona
- **In Review:** PR creado y asignado a reviewer. Máximo 24h en esta columna
- **QA:** Testing manual o automatizado. Si falla, regresa a In Progress
- **Done:** Cumple el Definition of Done. Desplegado o listo para deploy

#### 4.4 Métricas Kanban

| Métrica | Definición | Para qué sirve |
|---|---|---|
| **Lead Time** | Tiempo total desde que se solicita un ítem hasta que se entrega | Mide el tiempo de respuesta al cliente |
| **Cycle Time** | Tiempo desde que se empieza a trabajar un ítem hasta que se termina | Mide la eficiencia del equipo |
| **Throughput** | Cantidad de ítems completados por unidad de tiempo | Mide la capacidad de entrega |
| **Cumulative Flow Diagram (CFD)** | Gráfico de área que muestra ítems en cada estado a lo largo del tiempo | Detecta cuellos de botella y tendencias |

**Relación entre métricas:**
- Si Lead Time >> Cycle Time → los ítems esperan mucho antes de empezar (problema de priorización o capacidad)
- Si throughput baja → verificar WIP limits y cuellos de botella en el CFD
- Si una banda del CFD se ensancha → cuello de botella en esa columna

#### 4.5 Tabla comparativa: Scrum vs. Kanban

| Aspecto | Scrum | Kanban |
|---|---|---|
| **Cadencia** | Sprints fijos (1-4 semanas) | Flujo continuo, sin iteraciones fijas |
| **Roles** | PO, SM, Dev Team (obligatorios) | Sin roles prescriptos |
| **Ceremonias** | Planning, Daily, Review, Retro | Opcionales (standups, service reviews) |
| **Planificación** | Sprint Planning al inicio de cada sprint | Just-in-time: se toma el siguiente ítem del backlog |
| **Compromiso** | Sprint Backlog comprometido | Sin compromiso fijo; se gestiona por WIP limits |
| **Métricas** | Velocity, Burndown | Lead Time, Cycle Time, Throughput, CFD |
| **Cambios** | No se cambia el Sprint Backlog (salvo negociación) | Los ítems pueden cambiar en cualquier momento |
| **Estimación** | Story Points (Planning Poker) | Opcional; se puede medir por throughput |
| **Cuándo usar** | Proyectos con entregas regulares, equipos estables | Soporte, ops, trabajo con demanda variable |

#### 4.6 Cuándo elegir Kanban sobre Scrum

- **Equipos de soporte/ops** con demanda continua e impredecible
- **Mantenimiento de software** donde los bugs llegan todo el tiempo
- **Equipos con flujo continuo** que no se benefician de iteraciones fijas
- **Equipos en transición** que quieren empezar con algo más simple que Scrum
- **Trabajo de DevOps/SRE** donde el timebox de sprint no tiene sentido

---

### Sección 5 — Otras metodologías ágiles (resumen)

#### 5.1 XP (Extreme Programming)

**Creador:** Kent Beck (1996). XP es la metodología ágil más prescriptiva en prácticas técnicas.

**Prácticas clave:**

| Práctica | Descripción |
|---|---|
| **Pair Programming** | Dos programadores trabajan juntos en la misma estación. Uno escribe código, el otro revisa en tiempo real. |
| **TDD (Test-Driven Development)** | Escribir el test antes que el código. Ciclo: Red → Green → Refactor. |
| **Continuous Integration** | Integrar código al repositorio compartido múltiples veces al día. |
| **Refactoring** | Mejorar la estructura del código sin cambiar su comportamiento. Continuamente. |
| **Collective Ownership** | Todo el equipo es dueño de todo el código. Cualquiera puede modificar cualquier parte. |
| **Simple Design** | La solución más simple que funcione. No anticipar necesidades futuras (YAGNI). |
| **Releases pequeñas** | Entregas frecuentes y pequeñas en vez de releases grandes. |
| **Estándares de código** | Convenciones compartidas para que el código sea legible por todos. |

#### 5.2 SAFe (Scaled Agile Framework)

**Cuándo aplica:** Organizaciones con 3 o más equipos ágiles que necesitan coordinarse para entregar un producto o portfolio.

**Conceptos clave:**

| Concepto | Descripción |
|---|---|
| **PI Planning** | Program Increment Planning. Evento de 2 días donde todos los equipos sincronizan objetivos para las próximas 8-12 semanas. |
| **ART (Agile Release Train)** | Equipo de equipos (5-12 equipos) que trabajan en un mismo flujo de valor. |
| **Release Train** | Cadencia fija de entregas alineada con el PI. |
| **RTE (Release Train Engineer)** | El Scrum Master del ART — facilita la coordinación entre equipos. |

#### 5.3 LeSS (Large-Scale Scrum)

**Cuándo aplica:** Organizaciones que quieren escalar Scrum de forma minimalista (2-8 equipos trabajando en el mismo producto).

**Diferencia con SAFe:**
- LeSS es Scrum aplicado a escala, sin agregar capas de gestión
- SAFe agrega roles, ceremonias y artefactos adicionales
- LeSS tiene un solo Product Backlog y un solo PO para todos los equipos
- SAFe permite múltiples backlogs coordinados

#### 5.4 Scrumban

**Qué es:** Combinación de Scrum + Kanban. Mantiene la estructura de sprints de Scrum pero incorpora WIP limits y flujo continuo de Kanban.

**Cuándo usarlo:**
- Equipos Scrum que quieren mejorar su flujo sin abandonar sprints
- Equipos que necesitan más flexibilidad que Scrum puro pero más estructura que Kanban
- Transición gradual de Scrum a Kanban (o viceversa)

#### 5.5 Tabla comparativa rápida

| Aspecto | XP | Scrum | Kanban | SAFe | LeSS |
|---|---|---|---|---|---|
| **Escala** | 1 equipo | 1 equipo | 1 equipo | Multi-equipo (3-125+) | Multi-equipo (2-8) |
| **Foco** | Prácticas técnicas | Proceso y ceremonias | Flujo de trabajo | Coordinación organizacional | Scrum escalado minimalista |
| **Iteraciones** | 1-2 semanas | 1-4 semanas | Sin iteraciones | PI de 8-12 semanas | Sprints Scrum |
| **Roles** | Coach, Tracker, Customer | PO, SM, Dev Team | Sin roles fijos | Muchos (RTE, Product Mgmt, etc.) | PO, SM, equipos |
| **Prescripción** | Alta (prácticas técnicas) | Media (proceso) | Baja (principios) | Muy alta (framework completo) | Baja (Scrum + reglas) |
| **Ideal para** | Equipos técnicos maduros | Mayoría de equipos de desarrollo | Soporte, ops, mantenimiento | Grandes organizaciones | Organizaciones medianas |

---

### Sección 6 — User Stories, Épicas y Tareas

#### 6.1 Formato estándar de User Story

```
Como [rol], quiero [acción], para [beneficio]
```

**Ejemplo del proyecto:**
> Como desarrollador, quiero parsear templates DSL JSON, para alimentar el AST del motor  
> — US-05 del `../docs/06_backlog-tecnico/product-backlog_v1.0.md`

El formato establece:
- **Quién** necesita la funcionalidad (rol)
- **Qué** necesita hacer (acción)
- **Por qué** lo necesita (beneficio / valor de negocio)

#### 6.2 Criterios INVEST

Una buena User Story cumple los criterios INVEST:

| Criterio | Significado | Ejemplo ✅ | Ejemplo ❌ |
|---|---|---|---|
| **I**ndependiente | No depende de otras US para entregarse | US-03: Parser DSL puede entregarse sin rendering | "Implementar UI" que necesita backend primero |
| **N**egociable | Los detalles se negocian con el PO | El formato del DSL puede ajustarse durante el sprint | "Debe usar exactamente esta librería" |
| **V**aliosa | Aporta valor medible al usuario o negocio | "Renderizar ESC/POS para imprimir tickets" | "Refactorizar clase interna" (es tarea técnica) |
| **E**stimable | El equipo puede estimar su esfuerzo | "Parser DSL básico" → 13 SP | "Mejorar el sistema" → ¿cuánto es eso? |
| **S**mall | Lo suficientemente pequeña para un sprint | US-09: Renderizar ESC/POS (1 sprint) | "Implementar todo el motor" (épica entera) |
| **T**estable | Se puede verificar si está terminada | "Given DSL input, When parse, Then AST válido" | "El sistema debe ser rápido" |

#### 6.3 Criterios de aceptación: formato Given/When/Then

Los criterios de aceptación se escriben en formato BDD (Behavior-Driven Development):

```
Given [precondición / contexto]
When  [acción que ejecuta el usuario o el sistema]
Then  [resultado esperado observable]
```

**Ejemplo del proyecto (US-03: Parser DSL básico):**

```
Given una plantilla DSL JSON válida con un TextNode
When  el parser procesa la plantilla
Then  se genera un AST con un DocumentNode raíz y un TextNode hijo

Given una plantilla DSL JSON con sintaxis inválida
When  el parser intenta procesarla
Then  se lanza una excepción descriptiva con la ubicación del error
```

#### 6.4 Jerarquía: Iniciativa → Épica → User Story → Sub-tarea → Bug

```
Iniciativa (Tema estratégico)
    └── Épica (funcionalidad grande, multi-sprint)
            └── User Story (valor entregable en un sprint)
                    └── Sub-tarea / Tarea técnica (trabajo implementable)
                            └── Bug (defecto encontrado)
```

**Ejemplo concreto del proyecto:**

| Nivel | ID | Descripción |
|---|---|---|
| **Iniciativa** | NB-01 | Desacoplamiento datos/diseño — Necesidad de negocio |
| **Épica** | ÉPICA 3 | Parser DSL — Convertir DSL → AST |
| **User Story** | US-05 | Como desarrollador, quiero resolver datos dinámicos en el AST, para vincular datos externos a plantillas |
| **Sub-tarea (BT)** | BT-020 | Implementar IDslParser |
| **Sub-tarea (BT)** | BT-021 | Definir gramática DSL base |
| **Sub-tarea (BT)** | BT-022 | Implementar tokenizer / lexer |
| **Bug** | BUG-001 | Parser no maneja correctamente caracteres Unicode en TextNode |

> **Referencia:** Las épicas y user stories están en `../docs/06_backlog-tecnico/product-backlog_v1.0.md`. Las sub-tareas técnicas (BT-XXX) en `../docs/06_backlog-tecnico/backlog-tecnico_v1.0.md`.

#### 6.5 Estimación

##### Story Points vs. Horas

| Aspecto | Story Points | Horas |
|---|---|---|
| **Mide** | Complejidad relativa | Tiempo absoluto |
| **Ventaja** | Abstracto, no penaliza diferencias de skill | Fácil de entender para no-técnicos |
| **Desventaja** | Requiere calibración del equipo | Estimaciones inexactas, presión por cumplir |
| **Uso recomendado** | Planificación de sprints, velocity | Tracking personal, timeboxing de spikes |

##### Planning Poker

Técnica de estimación grupal:
1. El PO presenta la historia
2. Cada miembro del equipo elige una carta con su estimación (escala Fibonacci)
3. Se revelan todas las cartas simultáneamente
4. Si hay diferencias grandes, los extremos explican su razonamiento
5. Se repite hasta converger

**Escala Fibonacci:** 1, 2, 3, 5, 8, 13, 21, ∞, ☕

| Puntos | Significado típico |
|---|---|
| 1-2 | Tarea trivial, cambio menor |
| 3-5 | Complejidad moderada, bien entendida |
| 8 | Complejidad alta, alguna incertidumbre |
| 13 | Muy complejo, considerar descomponer |
| 21+ | Demasiado grande, DEBE descomponerse |
| ∞ | No se puede estimar — falta información |
| ☕ | Necesitamos un break |

**Ejemplo del proyecto:** En el Sprint 01, US-03 (Parser DSL básico) fue estimada en 13 SP — la más compleja del sprint, reflejando la incertidumbre del diseño del tokenizer.

#### 6.6 Priorización

##### MoSCoW

| Categoría | Significado | Distribución sugerida | Ejemplo del proyecto |
|---|---|---|---|
| **Must Have** | Imprescindible. Sin esto, el release no tiene sentido | ~60% del esfuerzo | US-03 (Parser DSL), US-09 (Render ESC/POS) |
| **Should Have** | Importante, pero el producto funciona sin esto | ~20% del esfuerzo | US-10 (Render texto plano), US-11 (Vista previa UI) |
| **Could Have** | Deseable si sobra capacidad | ~20% del esfuerzo | US-27 (Render PDF) |
| **Won't Have** | Explícitamente fuera de alcance para esta versión | 0% | Editor visual, scripting avanzado |

##### WSJF (Weighted Shortest Job First)

Fórmula de priorización de SAFe:

$$WSJF = \frac{\text{Valor de negocio} + \text{Criticidad temporal} + \text{Reducción de riesgo}}{\text{Tamaño del trabajo}}$$

Se usa para comparar ítems del backlog: el ítem con mayor WSJF se hace primero.

##### Value vs. Effort

Matriz 2x2 para priorización rápida:

```
                        VALOR ALTO
                            │
              ┌─────────────┼─────────────┐
              │  HACER       │  HACER       │
              │  DESPUÉS     │  PRIMERO     │
              │  (Big Bets)  │  (Quick Wins)│
  ESFUERZO ───┼─────────────┼─────────────┤─── ESFUERZO
    ALTO      │  NO HACER    │  HACER SI    │     BAJO
              │  (Money Pit) │  SOBRA TIEMPO│
              │              │  (Fill-Ins)  │
              └─────────────┼─────────────┘
                            │
                        VALOR BAJO
```

---

### Sección 7 — Métricas ágiles

#### 7.1 Velocity

**Qué es:** La cantidad de Story Points que el equipo completa por sprint. Es la métrica ágil más usada en Scrum.

**Cómo se calcula:** Suma de SP de todas las historias que cumplen el DoD al final del sprint.

**Cómo se usa para planificar:**
- Se toma el promedio de los **últimos 3 sprints** como referencia
- No se comprometen más SP que la velocity promedio (máximo 110%)
- Se usa para proyectar la fecha de finalización del release

**Referencia del proyecto:** `../docs/07_plan-sprint/velocidad-equipo_v1.0.md`

El proyecto registra velocity por sprint:

| Sprint | SP Comprometidos | SP Completados | Velocity |
|---|---|---|---|
| Sprint 01 | 48 | Pendiente | - |
| Sprint 02 | 76 | Pendiente | - |
| Sprint 03 | 77 | Pendiente | - |

> La velocity promedio se calcula con los últimos 3 sprints completados. Las variaciones significativas (>20%) deben analizarse en la retrospectiva.

#### 7.2 Burndown Chart

**Sprint Burndown:** Muestra los SP restantes del sprint a lo largo del tiempo.

```
SP restantes
    │
 40 │ ●
    │   ●
 30 │     ●                        Línea ideal
    │       ●  - - - - - - - - - -
 20 │         ●    ●
    │              ●               Línea real
 10 │                  ●
    │                    ●  ●
  0 │─────────────────────────●──
    └─────────────────────────────
     D1  D2  D3  D4  D5  D6  D7  D8  D9  D10
```

**Señales de alerta:**
- Línea real muy por encima de la ideal → riesgo de no completar el sprint
- Línea plana varios días → bloqueo o trabajo no descompuesto
- Caída súbita al final → historias NO se cierran incrementalmente

**Release Burndown:** Lo mismo pero a nivel de release. Muestra SP restantes del backlog completo, sprint a sprint.

#### 7.3 Burnup Chart

Inverso del burndown: muestra SP completados acumulados. Más útil cuando el scope cambia:

```
SP completados
    │                                    ─── Scope total
 200│                          ┌─────────
    │                   ┌──────┘
 150│            ┌──────┘
    │     ┌──────┘         ●
 100│  ┌──┘           ●
    │  │         ●                       ─── SP completados
 50 │  │    ●
    │  ●
  0 │──
    └─────────────────────────────
     S01  S02  S03  S04  S05  S06
```

Cuando la línea de scope sube, se agregó trabajo. Cuando las líneas convergen, se proyecta la fecha de finish.

#### 7.4 Cumulative Flow Diagram (CFD)

Muestra cuántos ítems hay en cada estado a lo largo del tiempo. Las bandas deben tener ancho estable. Si una banda se ensancha, hay un cuello de botella.

```
Ítems
    │
 50 │░░░░░░░░░░░░░░░░░░░░░░░░░░░  Done
    │▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓    In QA
 40 │████████████████████████       In Review
    │▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒          In Progress
 30 │░░░░░░░░░░░░░░░░              Backlog
    │
 20 │
    │
 10 │
    │
  0 │──────────────────────────────
    └──────────────────────────────
     Semana 1    Semana 2    Semana 3
```

#### 7.5 Lead Time y Cycle Time

```
                Lead Time
    ◄───────────────────────────────────►
    │                                   │
    │         Cycle Time                │
    │    ◄──────────────────────►       │
    │    │                      │       │
────┼────┼──────────────────────┼───────┼────
  Creado │                      │     Entregado
         │                      │
     Se empieza            Se termina
     a trabajar            de trabajar
```

#### 7.6 Tabla resumen de métricas

| Métrica | Qué mide | Frecuencia | Quién la usa |
|---|---|---|---|
| **Velocity** | SP completados por sprint | Cada sprint | SM, PO (planning) |
| **Sprint Burndown** | SP restantes durante el sprint | Diario | Dev Team, SM |
| **Release Burndown** | SP restantes del release | Cada sprint | PO, Stakeholders |
| **Burnup** | SP completados acumulados vs. scope | Cada sprint | PO, Stakeholders |
| **CFD** | Distribución de ítems por estado en el tiempo | Continuo | SM (detectar cuellos de botella) |
| **Lead Time** | Tiempo desde solicitud hasta entrega | Continuo | PO, Stakeholders |
| **Cycle Time** | Tiempo desde inicio de trabajo hasta fin | Continuo | Dev Team, SM |
| **Throughput** | Ítems completados por unidad de tiempo | Semanal | SM, PO |
| **Sprint Goal Completion** | % de sprints con goal cumplido | Cada sprint | SM, Stakeholders |

---

### Sección 8 — Anti-patrones ágiles

#### 8.1 Anti-patrones del backlog y gestión

Fuente: `../devs/especialidades/AG-06-scrum-master.md`

| Anti-patrón | Problema | Solución |
|---|---|---|
| **US como tarea técnica** | "Implementar Parser" no tiene valor para el usuario | Reformular como: "Como dev, quiero interpretar DSL, para generar documentos" |
| **Épicas sin descomponer** | Una épica de 40 SP en un sprint de 15 | Descomponer en US de 3-8 SP |
| **Sin MoSCoW** | Todo es "Must" → no hay priorización real | Forzar distribución: 60% Must, 20% Should, 20% Could |
| **DoR excesivo** | 15 criterios → nada nunca está "ready" | Máximo 6-8 criterios prácticos |
| **Backlog técnico oculto** | La deuda técnica no está visible para el PO | Registrar como ítems priorizables en el backlog |
| **Sin trazabilidad US→CU** | No se puede validar completitud del sistema | Columna "CU relacionados" obligatoria en cada US |

#### 8.2 Anti-patrones de sprints y ceremonias

Fuente: `../devs/especialidades/AG-07-gestion-proyectos-agiles.md`

| Anti-patrón | Problema | Solución |
|---|---|---|
| **Sprint Goal = lista de tareas** | "Implementar A, B, C" no da dirección ni prioridad | Reformular como frase de valor: "El motor procesa DSL end-to-end" |
| **DoD redefinido por sprint** | Cada sprint inventa su DoD → inconsistencia | Referenciar DoD canónico + agregar criterios específicos |
| **Overcommitment** | Más SP que la velocity promedio | Regla: nunca comprometer > 110% de velocity promedio |
| **Sin riesgos** | No se identifican riesgos → no hay plan B | Mínimo 2 riesgos por sprint con mitigación |
| **Retro sin acciones** | Se habla mucho pero no se define nada concreto | Cada retro debe producir ≥ 1 acción con responsable |
| **Velocity no registrada** | No se sabe cuánto puede el equipo | Actualizar tabla después de cada sprint review |

#### 8.3 Anti-patrones adicionales comunes

| Anti-patrón | Problema | Solución |
|---|---|---|
| **El PO ausente** | El Product Owner aparece solo en el planning y desaparece hasta la review. Las dudas no se resuelven, el equipo asume o se bloquea. | El PO debe estar disponible durante el sprint. Mínimo: atender dudas en el día, asistir a dailies 2-3 veces por semana. |
| **La daily de 45 minutos** | La daily se convierte en reunión de estado detallado, discusión técnica o resolución de problemas. | Timebox estricto de 15 minutos. Solo 3 preguntas: qué hice, qué haré, qué me bloquea. Discusiones técnicas → "parking lot" después de la daily. |
| **Sprint 0 eterno** | El equipo pasa semanas o meses en "preparación" (infra, diseño, setup) sin entregar incremento de producto. | Sprint 0 máximo de 1 sprint. Entregar algo funcional desde el Sprint 1, aunque sea mínimo. Setup de infra se puede hacer en paralelo. |
| **La retro sin acción** | La retrospectiva se convierte en sesión de catarsis donde todos hablan pero nadie se compromete a mejorar. | Cada retro produce mínimo 1 acción concreta con: responsable, fecha y sprint target. Revisar acciones anteriores al inicio de cada retro. |
| **Velocity como KPI de performance individual** | Se usa la velocity para evaluar la productividad de personas individuales, generando inflación de estimaciones y competencia tóxica. | Velocity es una métrica del EQUIPO para planificación. Nunca se usa para evaluar individuos. Si alguien entrega menos SP, se analiza en la retro como equipo, no como performance review. |
| **Micromanagement disfrazado de Scrum** | Un "Scrum Master" o manager asigna tareas, controla horarios y decide quién hace qué. El equipo no se auto-organiza. | El SM facilita, no gestiona. El equipo decide cómo hacer el trabajo. El SM remueve impedimentos y protege al equipo de interrupciones externas. |
| **El sprint elástico** | El sprint se extiende "unos días más" para completar las historias comprometidas. | El sprint tiene fecha fija. Lo que no se completó vuelve al backlog y se reprioriza. Nunca se extiende el timebox. |
| **El refinamiento inexistente** | No se hace refinamiento del backlog. Las historias llegan al planning sin detallar, sin estimar y sin criterios de aceptación. | Dedicar 10% del sprint a refinamiento (ej: 1-2 horas semanales). Las historias deben cumplir el DoR antes del planning. |
| **El board fantasma** | El board de Jira/tablero no refleja la realidad. Los ítems no se actualizan, las columnas no representan el estado real. | Actualizar el board en la daily. Si no está en el board, no existe. El SM revisa el board diariamente. |

---

## PARTE 2 — GESTIÓN DE TAREAS CON JIRA

---

### Sección 9 — Introducción a Jira

#### 9.1 Qué es Jira

**Jira** es una herramienta de gestión de proyectos desarrollada por **Atlassian**. Es la plataforma más usada en la industria del software para tracking de tareas, gestión de backlogs, planificación de sprints y seguimiento de bugs.

Jira permite:
- Crear y gestionar proyectos ágiles (Scrum y Kanban)
- Definir backlogs con épicas, historias, tareas y bugs
- Planificar y ejecutar sprints
- Visualizar el trabajo en tableros (boards)
- Generar reportes y métricas (velocity, burndown, CFD)
- Integración con Git, CI/CD y herramientas de comunicación

#### 9.2 Conceptos base

| Concepto | Definición |
|---|---|
| **Proyecto** | Contenedor de todo el trabajo. Tiene una clave única (ej: MDSL) que prefija todos los issues. |
| **Board** | Vista visual del trabajo. Puede ser Scrum (con sprints) o Kanban (flujo continuo). |
| **Backlog** | Vista de lista de todos los issues del proyecto, priorizados por orden. |
| **Sprint** | Iteración timeboxed en un proyecto Scrum. Se crea, se llena de issues, se inicia y se cierra. |
| **Issue** | Unidad de trabajo. Puede ser Epic, Story, Task, Sub-task o Bug. |
| **Workflow** | Flujo de estados que un issue recorre (To Do → In Progress → Done). |
| **Component** | Categoría para agrupar issues por módulo o subsistema (ej: Parser, Rendering, Core). |
| **Fix Version** | Versión del producto donde se incluirá el issue (ej: v1.0.0). Equivale a un Release/Milestone. |

#### 9.3 Tipos de proyecto

| Tipo | Descripción | Cuándo usar |
|---|---|---|
| **Scrum** | Board con backlog, sprints, velocity, burndown | Equipos con iteraciones fijas y ceremonias Scrum |
| **Kanban** | Board con flujo continuo, WIP limits, CFD | Equipos de soporte, ops o con demanda continua |
| **Team-managed** | Proyecto simple, configurado por el equipo | Equipos pequeños que quieren autonomía rápida |
| **Company-managed** | Proyecto administrado por admins de Jira | Organizaciones con governance y configuraciones centralizadas |

#### 9.4 Cuándo usar Jira vs. alternativas

| Herramienta | Fortaleza | Cuándo elegirla |
|---|---|---|
| **Jira** | Completísima para Scrum/Kanban, reportes avanzados, JQL, integraciones enterprise | Equipos medianos/grandes, organizaciones con procesos ágiles maduros |
| **Azure DevOps** | Integración nativa con ecosistema Microsoft (.NET, Azure, VS) | Equipos .NET/Azure, organizaciones Microsoft |
| **Linear** | UX moderna, velocidad, developer-friendly | Startups, equipos técnicos que priorizan DX |
| **Trello** | Simplicidad, tableros Kanban, gratuito | Equipos pequeños, proyectos simples, personas no-técnicas |
| **GitHub Projects** | Integración directa con repos y PRs, gratuito | Proyectos open source, equipos que viven en GitHub |

---

### Sección 10 — Nomenclatura y tipos de issue en Jira

#### 10.1 Tipos de issue estándar

##### Epic

- **Definición:** Funcionalidad grande que abarca múltiples historias y puede extenderse a varios sprints
- **Cuándo crear una:** Cuando hay un bloque de funcionalidades relacionadas que forman un objetivo de negocio coherente
- **Nomenclatura sugerida:** Se usa la clave del proyecto + número auto-incremental. Agregar título descriptivo
- **Ejemplo:** `MDSL-E03 — Parser DSL` (equivale a ÉPICA 3 del proyecto)

##### Story (User Story)

- **Formato:** "Como [rol], quiero [acción], para [beneficio]"
- **Campos obligatorios:** Summary, Description (con formato US), Acceptance Criteria, Epic Link, Story Points, Priority
- **Link a épica:** Toda story debe estar vinculada a una Epic
- **Ejemplo:** `MDSL-05 — Como desarrollador, quiero resolver datos dinámicos en el AST, para vincular datos externos a plantillas`

##### Task

- **Cuándo usar task vs. story:** Usar Task para trabajo que no tiene valor directo para el usuario final pero es necesario (infraestructura, configuración, spikes técnicos)
- **Ejemplo:** `MDSL-TK01 — Crear solución .sln y proyectos (Core, Parser, etc.)`

##### Sub-task

- **Para descomposición técnica:** Se crean bajo una Story o Task para representar el trabajo implementable
- **Ejemplo:** `MDSL-BT020 — Implementar IDslParser` (sub-task de la Story US-05)

##### Bug

- **Campos específicos:**
  - Pasos para reproducir (Steps to Reproduce)
  - Resultado esperado (Expected Result)
  - Resultado actual (Actual Result)
  - Severidad: Critical / Major / Minor / Trivial
  - Entorno: SO, versión del runtime, dispositivo
- **Ejemplo:** `MDSL-BUG003 — Parser no detecta nodos duplicados en templates con más de 3 niveles de anidamiento`

#### 10.2 Campos clave de cada issue

| Campo | Descripción | Obligatorio |
|---|---|---|
| **Summary** | Título conciso del issue | Sí |
| **Description** | Detalle, formato US, criterios de aceptación | Sí |
| **Assignee** | Miembro del equipo responsable | Sí (durante el sprint) |
| **Reporter** | Quien creó el issue | Auto (creador) |
| **Priority** | Highest, High, Medium, Low, Lowest | Sí |
| **Labels** | Etiquetas libres para categorizar (ej: tech-debt, refactor) | Opcional |
| **Components** | Módulo del sistema (ej: Parser, Rendering, Core) | Recomendado |
| **Sprint** | Sprint al que está asignado | Sí (cuando se compromete) |
| **Story Points** | Estimación de complejidad | Sí (para Stories) |
| **Fix Version** | Release donde se incluirá | Recomendado |
| **Epic Link** | Épica padre | Sí (para Stories y Tasks) |

#### 10.3 Prioridades en Jira y mapeo a MoSCoW

| Prioridad Jira | Icono | Mapeo MoSCoW | Uso |
|---|---|---|---|
| **Highest** | 🔴 | Must Have | Bloqueante. Sin esto, el release no sale. |
| **High** | 🟠 | Must Have | Crítico pero no bloqueante inmediato. |
| **Medium** | 🟡 | Should Have | Importante. Se incluye si hay capacidad. |
| **Low** | 🔵 | Could Have | Deseable. Se hace si sobra tiempo. |
| **Lowest** | ⚪ | Won't Have | No se hará en esta versión. Documentado para futuro. |

#### 10.4 Estados y workflow típico

```
┌──────────┐    ┌─────────────┐    ┌───────────┐    ┌─────┐    ┌──────┐
│  TO DO   │───►│ IN PROGRESS │───►│ IN REVIEW │───►│ QA  │───►│ DONE │
└──────────┘    └─────────────┘    └───────────┘    └─────┘    └──────┘
                       │                  │              │
                       │                  │              │
                       ◄──────────────────┘              │
                       │     (cambios solicitados)       │
                       ◄─────────────────────────────────┘
                             (bug encontrado en QA)
```

**Personalización del workflow:**
- Agregar estado **Blocked** para impedimentos
- Agregar estado **Ready for QA** si QA es un equipo separado
- Agregar transición automática cuando se crea un PR (→ In Review)
- Validaciones en transición: ej. no pasar a Done sin PR mergeado

#### 10.5 Tabla de nomenclatura sugerida

| Tipo Jira | Nomenclatura SDD | Ejemplo | Descripción |
|---|---|---|---|
| Epic | ÉPICA-XX | ÉPICA-03 | Agrupación de funcionalidades relacionadas |
| Story | US-XXX | US-005 | User Story con valor para el usuario |
| Task | TK-XXX | TK-015 | Tarea técnica sin valor directo al usuario |
| Sub-task | BT-XXX | BT-012 | Descomposición técnica de una Story/Task |
| Bug | BUG-XXX | BUG-003 | Defecto encontrado en testing o producción |

---

### Sección 11 — Configuración de un proyecto Scrum en Jira

#### 11.1 Crear proyecto Scrum: paso a paso

1. **Ir a Projects → Create project**
2. **Seleccionar template:** Scrum
3. **Tipo:** Team-managed (para autonomía) o Company-managed (para governance)
4. **Nombre:** Motor DSL de Generación de Documentos
5. **Clave:** MDSL (esta clave prefica todos los issues: MDSL-1, MDSL-2, etc.)
6. **Acceso:** Restringido al equipo o abierto a la organización

#### 11.2 Configurar Board

**Columnas** (mapean al workflow):

| Columna | Mapea a estado | Descripción |
|---|---|---|
| TO DO | To Do | Issues listos para tomar (cumplen DoR) |
| IN PROGRESS | In Progress | Alguien está trabajando activamente |
| IN REVIEW | In Review | PR creado, esperando code review |
| QA | QA | Testing (manual o automatizado) |
| DONE | Done | Cumple Definition of Done |

**Swimlanes** (filas horizontales para agrupar):
- Por Epic: cada épica tiene su fila → visual por funcionalidad
- Por Assignee: cada persona tiene su fila → visual de carga
- Por Priority: separar Highest/High del resto

**Filtros rápidos** (quick filters útiles):
- Solo mis issues: `assignee = currentUser()`
- Bugs: `type = Bug`
- Sin estimar: `"Story Points" is EMPTY`
- Bloqueados: `status = Blocked OR labels = impediment`

#### 11.3 Configurar Backlog

- Activar la vista de Backlog en el Board settings
- Ordenar por prioridad (drag & drop o usando Priority field)
- Agrupar por Epic para visualización jerárquica
- Usar la sección "Backlog" (sin sprint) para ítems no planificados

#### 11.4 Crear y gestionar Sprints

1. **Crear Sprint:** En la vista Backlog, click en "Create Sprint"
2. **Nombrar:** Sprint 01, Sprint 02, etc.
3. **Agregar issues:** Arrastrar desde el Backlog al Sprint
4. **Iniciar Sprint:** Definir fechas de inicio y fin, Sprint Goal
5. **Durante el Sprint:** El Board muestra los issues del sprint activo
6. **Cerrar Sprint:** Al finalizar, Jira pregunta qué hacer con ítems no completados (mover al siguiente sprint o al backlog)

#### 11.5 Configurar Epics

- Crear Epics desde el Roadmap view o desde el Backlog
- Asignar color a cada Epic para identificación visual
- Vincular Stories a Epics usando el campo "Epic Link"
- Usar la vista **Timeline** (roadmap) para visualizar Epics en el tiempo

#### 11.6 Configurar Releases (Fix Versions)

1. Ir a **Project Settings → Releases** (o Versions)
2. Crear versiones alineadas con el roadmap:
   - v1.0.0 — MVP (Sprints 01-04)
   - v1.1.0 — Expansión (Sprints 05-06)
   - v1.3.0 — Madurez (Sprints 07-08)
3. Asignar cada issue a su Fix Version correspondiente

#### 11.7 Componentes

Crear componentes que mapeen a los módulos de la arquitectura:

| Componente | Descripción | Lead (opcional) |
|---|---|---|
| Core | Modelo AST, DocumentNode, nodos base | — |
| Parser | Tokenizer, lexer, IDslParser | — |
| Rendering | EscPosRenderer, TextRenderer, renderers | — |
| Layout | Motor de layout, posicionamiento | — |
| Extensibility | Sistema de plugins, DI | — |
| Testing | Tests unitarios, integración, fixtures | — |

---

### Sección 12 — Flujo de trabajo diario con Jira

#### 12.1 Sprint Planning en Jira

1. Abrir la vista **Backlog**
2. Revisar el Product Backlog priorizado con el PO
3. Verificar que las historias candidatas cumplen el **DoR** (checklist en cada issue)
4. Arrastrar historias al sprint recién creado
5. Estimar con Planning Poker (usar campo Story Points)
6. Definir el **Sprint Goal** en el campo del sprint
7. Verificar que los SP comprometidos no excedan la velocity promedio
8. Iniciar el sprint con fecha de inicio y fin

#### 12.2 Daily Scrum con Jira

- Abrir el **Board** del sprint activo
- Cada miembro revisa sus issues en el board:
  - ¿Qué moví ayer? (columna actual)
  - ¿Qué voy a mover hoy? (siguiente transición)
  - ¿Hay algo que me bloquea? (marcar como Blocked o agregar label `impediment`)
- El SM verifica que el board refleja la realidad
- Duración: 15 minutos máximo

#### 12.3 Durante el sprint

- **Actualizar estados:** Mover issues entre columnas al cambiar de estado
- **Registrar impedimentos:** Crear issue tipo Bug o agregar label `impediment`
- **Agregar sub-tasks:** Si surge trabajo adicional para una Story, agregar sub-tasks
- **Logging de trabajo:** Usar la función Log Work si se trackea tiempo
- **Comentarios:** Documentar decisiones y hallazgos en los comentarios del issue

#### 12.4 Sprint Review en Jira

1. Filtrar issues del sprint: `sprint = "Sprint XX"`
2. Revisar estados: ¿cuántos Done vs. no completados?
3. Para cada issue completado: demo al PO, registrar feedback
4. Para issues no completados: documentar razón, decidir si mover al siguiente sprint o al backlog
5. Registrar métricas en el template de Review (`../docs/07_plan-sprint/template-sprint-review_v1.0.md`)
6. Actualizar tabla de velocity (`../docs/07_plan-sprint/velocidad-equipo_v1.0.md`)

#### 12.5 Sprint Retrospective

1. Usar el template de Retro (`../docs/07_plan-sprint/template-sprint-retrospectiva_v1.0.md`)
2. Formato Start-Stop-Continue (u otro acordado)
3. Definir acciones de mejora concretas
4. **Crear issues para las acciones de mejora** en el backlog del próximo sprint
5. Revisar acciones del sprint anterior (sección 2.6 del template)

#### 12.6 Refinamiento en Jira

1. Abrir la vista **Backlog**, sección sin sprint
2. Revisar historias candidatas para los próximos 2 sprints
3. Detallar description y criterios de aceptación
4. Estimar Story Points (Planning Poker)
5. Verificar DoR (usar checklist del issue)
6. Si la historia es muy grande, descomponerla en varias Stories + Sub-tasks

#### 12.7 Diagrama del flujo diario con Jira

```
┌─────────────────────────────────────────────────────────────────────┐
│                    FLUJO DIARIO CON JIRA                            │
│                                                                     │
│  ┌──────────────┐                                                   │
│  │  DAILY SCRUM │  ◄── 15 min, frente al Board                     │
│  │  (mañana)    │                                                   │
│  └──────┬───────┘                                                   │
│         │                                                           │
│         ▼                                                           │
│  ┌──────────────────────────────────────────────────────────┐       │
│  │  DESARROLLO                                              │       │
│  │                                                          │       │
│  │  1. Tomar issue de TO DO → mover a IN PROGRESS           │       │
│  │  2. Crear branch: {CLAVE-ISSUE}-descripcion-corta        │       │
│  │  3. Desarrollar + tests                                  │       │
│  │  4. Crear PR → mover a IN REVIEW                         │       │
│  │  5. Code review aprobado → mover a QA                    │       │
│  │  6. Tests pasan → mover a DONE                           │       │
│  └──────┬───────────────────────────────────────────────────┘       │
│         │                                                           │
│         ▼                                                           │
│  ┌──────────────┐                                                   │
│  │  ACTUALIZAR  │  ◄── Al finalizar el día o al completar un issue  │
│  │  BOARD       │                                                   │
│  │  + COMENTAR  │                                                   │
│  └──────────────┘                                                   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

### Sección 13 — Reportes y métricas en Jira

#### 13.1 Velocity Chart

**Qué muestra:** SP comprometidos vs. SP completados por sprint.

**Cómo leerlo:**
- Barras azules por encima de barras verdes → overcommitment
- Barras verdes consistentes → equipo predecible
- Barras verdes creciendo gradualmente → equipo madurando
- Barras verdes muy variables → estimación inconsistente

**Ubicación en Jira:** Board → Reports → Velocity Chart

#### 13.2 Burndown Chart

**Qué muestra:** SP restantes del sprint a lo largo del tiempo.

**Señales de alerta:**
- Línea plana → trabajo bloqueado o no descompuesto
- Caída súbita al final → historias cerradas en batch, no incrementalmente
- Línea real por encima de la guía → riesgo de no completar el sprint
- Línea sube → se agregó scope al sprint (anti-patrón)

**Ubicación en Jira:** Board → Reports → Burndown Chart

#### 13.3 Sprint Report

**Qué incluye:**
- Issues completados vs. no completados
- SP comprometidos vs. completados
- Issues agregados o removidos during sprint
- Resumen de status para la review

**Ubicación en Jira:** Board → Reports → Sprint Report

#### 13.4 Cumulative Flow Diagram (CFD)

**Qué detecta:**
- Cuello de botella en Code Review → banda de "In Review" se ensancha
- Falta de capacidad de QA → banda de "QA" crece
- Backlog creciendo más rápido que la entrega → divergencia

**Ubicación en Jira:** Board → Reports → Cumulative Flow Diagram (solo Kanban boards por defecto; en Scrum, usar plugin o JQL + dashboard)

#### 13.5 Control Chart

**Qué muestra:** Cycle time de cada issue individual a lo largo del tiempo.

**Uso:** Identificar issues con cycle time anormalmente alto para investigar la causa (bloqueados, mal estimados, dependencias).

**Ubicación en Jira:** Board → Reports → Control Chart

#### 13.6 Dashboards personalizados

Crear un dashboard con widgets útiles:

| Widget | Qué muestra | Para quién |
|---|---|---|
| Sprint Burndown | Progreso del sprint actual | Dev Team, SM |
| Velocity Chart | Tendencia de velocity | SM, PO |
| Pie Chart (por Priority) | Distribución de prioridades | PO |
| Pie Chart (por Status) | Issues por estado | SM |
| Filter Results (bugs abiertos) | Lista de bugs sin resolver | Dev Team, QA |
| Two-Dimensional Filter (Assignee × Status) | Carga por persona y estado | SM |
| Created vs. Resolved | Ratio de creación vs. resolución | PO, Stakeholders |

#### 13.7 JQL (Jira Query Language)

JQL es el lenguaje de consultas de Jira. Permite filtrar issues con precisión:

| Consulta | JQL |
|---|---|
| Issues del sprint actual | `sprint in openSprints()` |
| Bugs sin resolver | `type = Bug AND resolution = Unresolved` |
| Stories sin estimar | `type = Story AND "Story Points" is EMPTY` |
| Issues bloqueados | `status = Blocked OR labels = impediment` |
| Trabajo completado en el último sprint | `sprint in closedSprints() AND status = Done ORDER BY updated DESC` |
| Issues de una épica específica | `"Epic Link" = MDSL-E03` |
| Issues creados esta semana | `created >= startOfWeek()` |
| Issues sin asignar en el sprint | `sprint in openSprints() AND assignee is EMPTY` |
| Issues con alta prioridad sin sprint | `priority in (Highest, High) AND sprint is EMPTY` |
| Deuda técnica | `labels = tech-debt AND resolution = Unresolved ORDER BY priority DESC` |

---

### Sección 14 — Hitos (Milestones) y Releases en Jira

#### 14.1 Fix Versions como Milestones

Jira no tiene un concepto nativo de "Milestone" como GitHub. En su lugar, se usan **Fix Versions** (también llamadas Releases) para representar hitos del producto.

Cada Fix Version tiene:
- **Nombre:** versión semántica (ej: v1.0.0)
- **Start date:** fecha de inicio
- **Release date:** fecha de entrega planificada
- **Description:** objetivo del release
- **Status:** Unreleased, Released, Archived

#### 14.2 Release Hub

Jira ofrece una vista de Release Hub (Deployments → Releases) donde se puede:

- **Planning:** Ver qué issues están asignados a cada versión
- **Tracking:** Progreso de completitud (% de issues Done)
- **Ship:** Marcar la versión como Released cuando se despliega

#### 14.3 Mapeo al roadmap del proyecto

Referencia: `../docs/00_contexto/roadmap-producto_v1.0.md`

| Fase | Release Jira | Sprints | Objetivo | Épicas |
|---|---|---|---|---|
| **Fase 1 — MVP** | v1.0.0 | Sprint 01-04 | Motor funcional DSL → AST → Render ESC/POS | ÉPICA 1-7 (parcial) |
| **Fase 2 — Expansión** | v1.1.0 / v1.2.0 | Sprint 05-06 | Multi-formato, extensibilidad, integración MAUI | ÉPICA 7 (completa), 8, 9 |
| **Fase 3 — Madurez** | v1.3.0 | Sprint 07-08 | PDF, Bluetooth, performance, documentación | ÉPICA 10, 11 |
| **Futuro** | v2.0.0 | Por definir | Breaking changes, DSL v2, editor visual | Por definir |

#### 14.4 Cómo vincular issues a releases

1. Abrir el issue en Jira
2. Campo **Fix Version**: seleccionar la versión correspondiente
3. En bulk: seleccionar múltiples issues → Bulk Change → Edit → Fix Version

#### 14.5 Release notes automáticas desde Jira

Al marcar una Fix Version como "Released":
1. Ir a **Project → Releases → [versión]**
2. Click en **Release notes**
3. Jira genera automáticamente una lista de issues completados, agrupados por tipo

#### 14.6 Tabla de mapeo completa SDD → Jira

| Concepto SDD | Equivalente Jira | Ejemplo del proyecto |
|---|---|---|
| Fase del roadmap | Fix Version (Release) | v1.0.0 — MVP |
| Épica | Epic | ÉPICA 3 — Parser DSL |
| User Story | Story | US-05: Resolver datos dinámicos en el AST |
| Backlog Técnico | Sub-task o Task | BT-012: Implementar nodos básicos |
| Sprint Plan | Sprint | Sprint 01 (2 semanas, 48 SP) |
| Necesidad de Negocio | Initiative/Theme (o Label) | NB-01: Desacoplamiento datos/diseño |
| Caso de Uso | Linked Issue o Label | CU-05: Procesar template DSL |
| Definition of Ready | Checklist en Story (o campo custom) | DoR checklist con 8 criterios |
| Definition of Done | Workflow transition conditions | Validaciones en transición a Done |
| Review del sprint | Sprint Report + filtro del sprint | Sprint Report de Jira + template de review |
| Retrospectiva | Issues de mejora en siguiente sprint | Acciones AM-XX como Tasks del sprint siguiente |
| Velocity | Velocity Chart de Jira | Charts auto-generados + velocidad-equipo_v1.0.md |

---

### Sección 15 — Integración Jira con herramientas del equipo

#### 15.1 Jira + Git (GitHub/GitLab/Bitbucket)

**Smart Commits:** Al incluir la clave del issue en los mensajes de commit, Jira vincula automáticamente el commit al issue:

```
git commit -m "MDSL-05 #comment Implementar DataResolver básico #time 2h"
```

Acciones disponibles en smart commits:
- `#comment [texto]` → agrega un comentario al issue
- `#time [duración]` → registra tiempo de trabajo
- `#[transición]` → cambia el estado (ej: `#done`, `#in-review`)

**Branch naming con clave de issue:**

Formato recomendado: `{CLAVE-ISSUE}-descripcion-corta`

| Tipo | Formato de rama | Ejemplo |
|---|---|---|
| Feature | `feature/MDSL-05-data-resolver` | `feature/MDSL-05-data-resolver` |
| Bugfix | `bugfix/MDSL-BUG003-unicode-parser` | `bugfix/MDSL-BUG003-unicode-parser` |
| Hotfix | `hotfix/MDSL-BUG007-crash-escpos` | `hotfix/MDSL-BUG007-crash-escpos` |

> **Referencia:** Ver la guía de flujo de trabajo y versionado del proyecto en `../devs/versionado/guia-flujo-trabajo-versionado.md`

**Beneficios de la integración:**
- En Jira, cada issue muestra las branches, commits y PRs asociados
- En GitHub/GitLab, el PR muestra el issue de Jira vinculado
- Trazabilidad completa: issue → branch → commits → PR → merge → deploy

#### 15.2 Jira + CI/CD

**Deployment tracking:**
- Jira puede mostrar en qué entorno está desplegado un issue (dev, staging, prod)
- Se configura desde la integración con GitHub Actions, GitLab CI, Azure Pipelines, etc.

**Build info:**
- Jira muestra el estado del build (pass/fail) asociado a cada issue
- Si el CI falla, el issue no debería transicionar a Done

**Configuración típica:**
1. Instalar la app de Jira en GitHub/GitLab
2. Configurar el pipeline para enviar deployment info a Jira
3. En Jira: ver Deployments tab en cada issue

#### 15.3 Jira + Confluence

- Vincular páginas de Confluence a issues de Jira (documentación técnica, ADRs, guías)
- Crear páginas desde templates: Sprint Plan, Review, Retro
- Usar macros de Jira en Confluence para embeber filtros JQL y reportes

#### 15.4 Jira + Slack/Teams

**Notificaciones útiles:**
- Issue asignado a mí → notificación personal
- Issue movido a Done → notificación al canal del equipo
- Bug creado con prioridad Highest → notificación urgente
- Sprint iniciado/cerrado → resumen al canal

**Configuración:**
1. Instalar la app de Jira para Slack/Teams
2. Conectar el proyecto
3. Configurar reglas de notificación por canal

#### 15.5 Automatizaciones útiles

Jira Automation permite reglas sin código:

| Automatización | Trigger | Acción |
|---|---|---|
| **Auto-assign** | Issue movido a In Progress | Asignar al usuario que movió el issue |
| **Auto-transition** | PR mergeado en GitHub | Mover issue a In Review o Done |
| **Notificación de bloqueo** | Issue marcado como Blocked | Enviar mensaje al SM por Slack |
| **Cierre de sprint** | Sprint cerrado | Enviar resumen de velocity al canal del equipo |
| **Sub-task done** | Todas las sub-tasks de una Story en Done | Transicionar la Story a In Review |
| **SLA warning** | Issue lleva > 3 días en In Progress | Notificación al assignee y SM |
| **Sprint scope alert** | Issue agregado al sprint activo | Notificación al SM y PO |

---

## Control de Cambios

| Versión | Fecha | Descripción |
|---|---|---|
| 1.0 | 2026-04-13 | Versión inicial — documento completo de referencia |

---

**Fin del documento**
