# Guía de Estudio — Cómo arrancar un proyecto con Scrum

**Documento:** guia-de-estudio.md  
**Versión:** 1.0  
**Fecha:** 2026-04-15  
**Contexto:** Guía práctica de estudio basada en ejemplos concretos para organizar un proyecto usando Scrum desde cero

---

## Índice

- [1. Punto de partida — ¿Cuándo estás listo para organizar el Scrum?](#1--punto-de-partida--cuándo-estás-listo-para-organizar-el-scrum)
- [2. Lo primero que debés construir: el Product Backlog](#2--lo-primero-que-debés-construir-el-product-backlog)
  - [Paso 1 — Formalizar la Visión del producto](#paso-1--formalizar-la-visión-del-producto)
  - [Paso 2 — Identificar las Épicas](#paso-2--identificar-las-épicas)
  - [Paso 3 — Construir el Product Backlog (User Stories + MoSCoW)](#paso-3--construir-el-product-backlog-user-stories--moscow)
  - [Paso 4 — Definir el DoR y el DoD](#paso-4--definir-el-dor-y-el-dod)
- [3. Ejemplos completos en tres contextos distintos](#3--ejemplos-completos-en-tres-contextos-distintos)
  - [Ejemplo A — Sistema de turnos para una clínica](#ejemplo-a--sistema-de-turnos-para-una-clínica)
  - [Ejemplo B — Sistema de inventario para ferretería](#ejemplo-b--sistema-de-inventario-para-ferretería)
  - [Ejemplo C — Plataforma de cursos online](#ejemplo-c--plataforma-de-cursos-online)
- [4. Cómo agrupar el backlog en épicas](#4--cómo-agrupar-el-backlog-en-épicas)
  - [Vista de mapeo: US por épica (clínica)](#vista-de-mapeo-us-por-épica-clínica)
  - [Vista consolidada por prioridad](#vista-consolidada-por-prioridad)
- [5. Criterios para definir una épica](#5--criterios-para-definir-una-épica)
- [6. El patrón que se repite](#6--el-patrón-que-se-repite)

---

## 1 — Punto de partida — ¿Cuándo estás listo para organizar el Scrum?

Antes de nombrar roles, crear tableros o escribir user stories, necesitás tener cubiertos estos insumos. No necesitan ser documentos formales — alcanza con que estén discutidos y acordados con el cliente:

| Insumo | Descripción | Equivale a... |
|---|---|---|
| **La idea y qué quiere el cliente** | Visión general del problema y del producto esperado | AG-00: Visión del producto |
| **Qué da y qué pide el sistema** | Entradas, salidas, flujos principales — los requerimientos | AG-01: Necesidades de negocio |
| **Cómo lo quiere el cliente** | Interfaces posibles: formularios, JSONs de ejemplo, capturas, reportes | AG-02/AG-03: Especificación funcional y UX |

Cuando tenés estos tres bloques discutidos, **el siguiente paso es organizar el Scrum**. Y lo primero que se construye es el **Product Backlog**.

---

## 2 — Lo primero que debés construir: el Product Backlog

El Product Backlog es la lista priorizada de todo lo que el sistema debe hacer. Es la única fuente de verdad para el equipo de desarrollo. Sin él no hay Sprint Planning, no hay velocity y no hay compromisos posibles.

Se construye en cuatro pasos secuenciales. Cada paso depende del anterior.

---

### Paso 1 — Formalizar la Visión del producto

La visión es una frase única que ancla todas las decisiones de priorización. Sin ella, cualquier feature parece igual de importante.

**Template:**
```
"Para [quién], que [necesita],
el sistema [nombre del producto] es [qué tipo de sistema]
que [beneficio clave],
a diferencia de [alternativa actual que el cliente usa hoy]."
```

**Criterio de calidad:** si la visión se puede aplicar a cualquier producto, es demasiado vaga. Debe ser específica al problema real del cliente.

---

### Paso 2 — Identificar las Épicas

Una **épica** es una capacidad funcional completa del sistema que es demasiado grande para completarse en un solo sprint. Se descompone en múltiples User Stories.

**Cantidad típica al inicio:** entre 4 y 8 épicas para un MVP.

**Cómo identificarlas:** tomá los requerimientos del cliente y preguntate: *¿qué grandes cosas debe poder hacer este sistema como unidad de valor completa?* Cada respuesta es una épica candidata.

```
Requerimientos del cliente
        ↓
¿Qué puede hacer el sistema como unidad completa?
        ↓
      Épicas
```

---

### Paso 3 — Construir el Product Backlog (User Stories + MoSCoW)

Cada épica se descompone en **User Stories** (US). Cada US describe una funcionalidad desde la perspectiva del usuario.

**Formato de User Story:**
```
Como [rol/actor],
quiero [acción concreta],
para [beneficio o razón].
```

Una vez escritas, se clasifican con **MoSCoW**:

| Prioridad | Significado | Criterio práctico |
|---|---|---|
| **Must Have** | Imprescindible para el MVP | Sin esto el sistema no cumple su propósito |
| **Should Have** | Importante pero no bloqueante | El MVP funciona sin esto, pero sería incompleto |
| **Could Have** | Deseable si hay capacidad | Agrega valor pero puede esperar a la v2 |
| **Won't Have v1** | Fuera de alcance por ahora | Documentado para no olvidar, pero no se construye |

> **Regla práctica:** si todo es Must Have, no hay priorización real. Forzate a que el Must Have sea el mínimo con el que el cliente ya resuelve su problema.

---

### Paso 4 — Definir el DoR y el DoD

Antes del primer sprint, el equipo debe acordar dos definiciones que gobiernan el flujo de trabajo:

**DoR — Definition of Ready**  
*¿Cuándo una User Story está lista para entrar a un sprint?*

Si una historia no cumple el DoR, no entra al Sprint Planning. Esto evita comprometer trabajo que no está lo suficientemente definido.

Criterios típicos de DoR:
- [ ] Tiene criterios de aceptación escritos (al menos 3 escenarios)
- [ ] Fue estimada en Story Points por el equipo
- [ ] Las dependencias técnicas están identificadas
- [ ] Los wireframes o diseños necesarios están disponibles
- [ ] El PO la aprobó como prioridad del sprint

**DoD — Definition of Done**  
*¿Cuándo una User Story está realmente terminada?*

Si una historia no cumple el DoD, no se puede marcar como cerrada. Esto evita la deuda técnica silenciosa.

Criterios típicos de DoD:
- [ ] El código fue revisado y aprobado en PR
- [ ] Tiene tests unitarios con cobertura ≥ 70%
- [ ] Pasa todos los tests en CI (build verde)
- [ ] Fue probada manualmente contra sus criterios de aceptación
- [ ] El PO la aceptó en la Sprint Review

> **Diferencia clave:**  
> DoR = condiciones para *empezar* a construir.  
> DoD = condiciones para *terminar* de construir.

---

## 3 — Ejemplos completos en tres contextos distintos

---

### Ejemplo A — Sistema de turnos para una clínica

#### Visión
> "Para **pacientes** que **necesitan sacar turno médico sin llamar por teléfono**, el sistema **TurnoYa** es una **aplicación web** que **permite reservar, cancelar y reprogramar turnos en tiempo real**, a diferencia de **llamar al consultorio en horario de atención y esperar en línea**."

#### Épicas

| ID | Épica | Capacidad del sistema |
|---|---|---|
| EP-01 | Registro y autenticación de pacientes | El sistema puede identificar quién entra |
| EP-02 | Búsqueda y reserva de turnos | El sistema puede gestionar reservas de tiempo |
| EP-03 | Gestión de agenda del profesional | El sistema puede gestionar la disponibilidad del médico |
| EP-04 | Notificaciones y recordatorios | El sistema puede comunicarse proactivamente |
| EP-05 | Historial de turnos | El sistema puede mostrar el pasado de un paciente |

#### Product Backlog

| ID | User Story | Épica | Prioridad |
|---|---|---|---|
| US-01 | Como paciente, quiero registrarme con email y contraseña, para poder acceder al sistema | EP-01 | Must Have |
| US-02 | Como paciente, quiero buscar turnos disponibles por especialidad y fecha, para elegir el que me conviene | EP-02 | Must Have |
| US-03 | Como paciente, quiero reservar un turno, para confirmar mi cita sin llamar | EP-02 | Must Have |
| US-04 | Como paciente, quiero cancelar un turno, para liberar el horario si no puedo asistir | EP-02 | Must Have |
| US-05 | Como médico, quiero ver mi agenda del día, para saber qué pacientes tengo | EP-03 | Must Have |
| US-06 | Como paciente, quiero recibir un recordatorio por email 24hs antes, para no olvidar el turno | EP-04 | Should Have |
| US-07 | Como paciente, quiero reprogramar un turno sin cancelarlo, para no perder mi lugar en la agenda | EP-02 | Should Have |
| US-08 | Como paciente, quiero ver mi historial de turnos anteriores, para recordar cuándo fui | EP-05 | Could Have |
| US-09 | Como médico, quiero bloquear franjas de mi agenda, para marcar vacaciones o reuniones | EP-03 | Could Have |
| US-10 | Como paciente, quiero iniciar sesión con Google, para no crear otra contraseña | EP-01 | Won't Have v1 |

#### DoR

Una US entra al sprint cuando:
- [ ] Tiene criterios de aceptación escritos (al menos 3)
- [ ] Está estimada en Story Points por el equipo
- [ ] Las dependencias técnicas están identificadas
- [ ] Los wireframes o mockups necesarios están disponibles
- [ ] El PO la aprobó como prioridad del sprint

#### DoD

Una US se considera terminada cuando:
- [ ] El código fue revisado y aprobado en PR
- [ ] Tiene tests unitarios con cobertura ≥ 70%
- [ ] Pasa todos los tests en CI
- [ ] Fue probada manualmente contra sus criterios de aceptación
- [ ] El PO la aceptó en la Sprint Review

---

### Ejemplo B — Sistema de inventario para ferretería

#### Visión
> "Para **dueños de ferreterías** que **necesitan controlar el stock sin planillas Excel**, el sistema **StockFácil** es una **aplicación de escritorio** que **permite gestionar entradas, salidas y alertas de stock mínimo en tiempo real**, a diferencia de **actualizar tablas manuales con riesgo de errores y desincronización**."

#### Épicas

| ID | Épica | Capacidad del sistema |
|---|---|---|
| EP-01 | Gestión del catálogo de productos | El sistema puede mantener el registro de productos |
| EP-02 | Movimientos de stock (entradas y salidas) | El sistema puede registrar el flujo de mercadería |
| EP-03 | Alertas y reportes | El sistema puede informar el estado del inventario |
| EP-04 | Gestión de proveedores | El sistema puede relacionar productos con sus fuentes de reposición |
| EP-05 | Usuarios y permisos | El sistema puede controlar quién hace qué |

#### Product Backlog

| ID | User Story | Épica | Prioridad |
|---|---|---|---|
| US-01 | Como encargado, quiero agregar un producto con nombre, código y precio, para tenerlo en el inventario | EP-01 | Must Have |
| US-02 | Como encargado, quiero registrar una entrada de stock, para actualizar la cantidad disponible | EP-02 | Must Have |
| US-03 | Como vendedor, quiero registrar una salida de stock, para descontar unidades al vender | EP-02 | Must Have |
| US-04 | Como dueño, quiero ver el stock actual de todos los productos, para saber qué tengo en el depósito | EP-01 | Must Have |
| US-05 | Como dueño, quiero recibir una alerta cuando un producto llega al stock mínimo, para generar el pedido a tiempo | EP-03 | Must Have |
| US-06 | Como dueño, quiero ver un reporte de movimientos por fecha, para auditar entradas y salidas | EP-03 | Should Have |
| US-07 | Como encargado, quiero cargar un proveedor con sus datos de contacto, para saber a quién llamar cuando necesito reponer | EP-04 | Should Have |
| US-08 | Como dueño, quiero exportar el inventario a Excel, para compartirlo con el contador | EP-03 | Could Have |
| US-09 | Como dueño, quiero asignar roles (vendedor / encargado), para limitar quién puede modificar precios | EP-05 | Could Have |
| US-10 | Como vendedor, quiero escanear código de barras para registrar salidas, para no tipear el código | EP-02 | Won't Have v1 |

#### DoR

- [ ] Tiene criterios de aceptación escritos
- [ ] Está estimada en Story Points
- [ ] El modelo de datos que afecta está identificado
- [ ] No tiene dependencias bloqueantes sin resolver
- [ ] El PO la aprobó como prioridad del sprint

#### DoD

- [ ] Código revisado en PR por al menos 1 persona
- [ ] Tests unitarios con cobertura ≥ 70% en la lógica de negocio
- [ ] Integración probada contra la base de datos real (no mock)
- [ ] Validado manualmente contra criterios de aceptación
- [ ] PO aceptó la funcionalidad en Sprint Review

---

### Ejemplo C — Plataforma de cursos online

#### Visión
> "Para **instructores independientes** que **necesitan vender cursos sin pagar comisiones a plataformas como Udemy**, el sistema **CursoPropio** es una **plataforma SaaS** que **permite publicar, vender y gestionar cursos con su propia marca**, a diferencia de **publicar en plataformas que se quedan con el 30-50% de cada venta y no ceden el control sobre los estudiantes**."

#### Épicas

| ID | Épica | Capacidad del sistema |
|---|---|---|
| EP-01 | Registro y perfiles (instructores y alumnos) | El sistema puede identificar y diferenciar actores |
| EP-02 | Creación y publicación de cursos | El sistema puede alojar y organizar contenidos |
| EP-03 | Inscripción y pagos | El sistema puede habilitar el acceso previo cobro |
| EP-04 | Reproducción de contenidos | El sistema puede entregar el aprendizaje |
| EP-05 | Progreso, certificados y evaluaciones | El sistema puede medir y acreditar el avance |
| EP-06 | Panel de analytics para el instructor | El sistema puede informar el desempeño comercial |

#### Product Backlog

| ID | User Story | Épica | Prioridad |
|---|---|---|---|
| US-01 | Como instructor, quiero registrarme y crear mi perfil, para tener mi espacio en la plataforma | EP-01 | Must Have |
| US-02 | Como instructor, quiero crear un curso con título, descripción y precio, para publicarlo | EP-02 | Must Have |
| US-03 | Como instructor, quiero subir videos y materiales por sección, para organizar el contenido | EP-02 | Must Have |
| US-04 | Como alumno, quiero registrarme e inscribirme a un curso, para acceder al contenido | EP-01 | Must Have |
| US-05 | Como alumno, quiero ver el contenido del curso que compré, para aprender | EP-04 | Must Have |
| US-06 | Como instructor, quiero gestionar el pago de inscripciones, para cobrar por mis cursos | EP-03 | Must Have |
| US-07 | Como alumno, quiero marcar lecciones como completadas, para llevar mi progreso | EP-05 | Should Have |
| US-08 | Como alumno, quiero recibir un certificado al completar el curso, para acreditar lo que aprendí | EP-05 | Should Have |
| US-09 | Como instructor, quiero ver cuántos alumnos tengo y cuánto recaudé, para evaluar el desempeño | EP-06 | Should Have |
| US-10 | Como alumno, quiero recibir notificaciones cuando hay nuevo contenido, para saber que hay actualizaciones | EP-04 | Could Have |
| US-11 | Como instructor, quiero aplicar descuentos o cupones de pago, para hacer promociones | EP-03 | Could Have |
| US-12 | Como alumno, quiero ver los cursos en modo offline descargados, para estudiar sin internet | EP-04 | Won't Have v1 |

#### DoR

- [ ] Tiene criterios de aceptación con al menos 3 escenarios (happy path + 2 edge cases)
- [ ] Estimada en Story Points (Planning Poker completado)
- [ ] Dependencias de integración (pagos, video hosting) identificadas
- [ ] Diseño de pantalla disponible para las US con UI
- [ ] No hay ambigüedad en el alcance: el PO aprobó los límites de la historia

#### DoD

- [ ] PR aprobado por al menos 2 reviewers
- [ ] Tests unitarios ≥ 70% cobertura + tests de integración para flujos críticos (pagos, acceso)
- [ ] CI/CD verde (build + test + linter)
- [ ] Probado en los 3 browsers objetivo (Chrome, Firefox, Safari)
- [ ] PO aceptó en Sprint Review
- [ ] Documentación de API actualizada si aplica

---

## 4 — Cómo agrupar el backlog en épicas

Una vez que tenés las US escritas, el agrupamiento en épicas no es arbitrario. Acá se muestra el mapeo completo del Ejemplo A para que quede claro el criterio:

### Vista de mapeo: US por épica (clínica)

#### EP-01 — Registro y autenticación de pacientes
- US-01 — Registrarse con email y contraseña *(Must Have)*
- US-10 — Iniciar sesión con Google *(Won't Have v1)*

#### EP-02 — Búsqueda y reserva de turnos
- US-02 — Buscar turnos disponibles *(Must Have)*
- US-03 — Reservar un turno *(Must Have)*
- US-04 — Cancelar un turno *(Must Have)*
- US-07 — Reprogramar un turno *(Should Have)*

#### EP-03 — Gestión de agenda del profesional
- US-05 — Ver agenda del día *(Must Have)*
- US-09 — Bloquear franjas de agenda *(Could Have)*

#### EP-04 — Notificaciones y recordatorios
- US-06 — Recordatorio por email 24hs antes *(Should Have)*

#### EP-05 — Historial de turnos
- US-08 — Ver historial de turnos anteriores *(Could Have)*

### Vista consolidada por prioridad

| Épica | Must Have | Should Have | Could Have | Won't Have v1 |
|---|---|---|---|---|
| EP-01 Autenticación | US-01 | — | — | US-10 |
| EP-02 Reserva de turnos | US-02, US-03, US-04 | US-07 | — | — |
| EP-03 Agenda médico | US-05 | — | US-09 | — |
| EP-04 Notificaciones | — | US-06 | — | — |
| EP-05 Historial | — | — | US-08 | — |

> **El MVP mínimo** de este sistema son las US Must Have de EP-01 y EP-02 (US-01 a US-05): con esas 5 historias el sistema ya resuelve el problema central — un paciente puede registrarse y reservar un turno sin llamar por teléfono.

---

## 5 — Criterios para definir una épica

La orientación al usuario es una consecuencia, no el criterio principal. El criterio real es la **capacidad funcional completa**.

### El criterio principal: capacidad funcional completa

Una épica responde a la pregunta:  
> **¿Qué puede hacer el sistema como unidad de valor completa e independiente?**

Cada respuesta es una épica candidata.

### Los tres criterios formales

**1. Independencia funcional**  
Si la capacidad se puede construir y desplegar sin afectar a otra, son épicas distintas.  
→ EP-04 (notificaciones) se puede implementar o no sin afectar EP-02 (reservas). Son independientes.

**2. Tamaño**  
Cada épica debe ser demasiado grande para completarse en un solo sprint. Si no lo es, es directamente una US.

**3. Cohesión interna**  
Las US dentro de una épica comparten:
- Las mismas entidades de datos
- Las mismas pantallas o flujos
- El mismo contexto de negocio

### Cuándo el usuario SÍ define la épica

En sistemas con roles muy distintos, es válido separar épicas por actor **si sus flujos son completamente independientes**:

```
EP-03 Agenda del médico    →  solo el médico opera aquí
EP-02 Reserva de turnos    →  solo el paciente opera aquí
```

Pero si dos actores operan sobre la **misma** capacidad (ej: el médico aprueba el turno que el paciente reservó), eso va en la misma épica porque comparten la misma capacidad funcional.

**Regla práctica:**
```
Primero identificá la capacidad → después fijate quién la usa
No al revés.
```

---

## 6 — El patrón que se repite

Independientemente del dominio (clínica, ferretería, cursos online), el patrón es siempre el mismo:

| Elemento | Pregunta que responde |
|---|---|
| **Visión** | ¿Por qué existe este sistema y para quién? |
| **Épicas** | ¿Qué grandes capacidades tiene el sistema? |
| **Must Have** | ¿Sin qué no hay MVP? |
| **Should Have** | ¿Qué lo hace completo pero no es bloqueante? |
| **Could Have** | ¿Qué agrega valor pero puede esperar a la v2? |
| **Won't Have v1** | ¿Qué está descartado por ahora (pero documentado)? |
| **DoR** | ¿Cuándo una historia está lista para construirse? |
| **DoD** | ¿Cuándo una historia está realmente terminada? |

Cuando estos ocho elementos están definidos, el equipo tiene todo lo necesario para ejecutar el primer Sprint Planning sin ambigüedad.

---

## Control de Cambios

| Versión | Fecha | Descripción |
|---|---|---|
| 1.0 | 2026-04-15 | Versión inicial — guía de estudio basada en ejemplos de arranque de proyectos Scrum |

---

**Fin del documento**
