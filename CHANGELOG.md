# Changelog

Todos los cambios notables de este proyecto se documentan en este archivo.

El formato sigue [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/),
y este proyecto adhiere a [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

Las versiones se determinan automáticamente desde [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) vía MinVer.

Los paquetes se distribuyen por GitHub Packages: `MotorDsl.Core`, `MotorDsl.Parser`, `MotorDsl.Rendering` y `MotorDsl.Extensions`.

---

## [Unreleased]

### Added

- Caso de ejemplo aplicado de metodologías ágiles bajo `docs/devs/metodos-agiles` (commit `ecb34db`).
- Guía de estudio operativa para Definition of Done y Definition of Ready (commit `36faf78`).
- Material de referencia sobre método Scrum dentro de la documentación de proceso (commit `38324f4`).
- Documentación operativa de metodologías ágiles y su integración con el flujo Git (commits `088ce82`, `cb1e2d7`).
- Sección `devs/` con documentación de soporte para contribuidores (commit `80355fd`).

### Changed

- Reorganización y ajustes de UX/UI sobre la documentación pública (commit `3c98923`).
- Actualización de la documentación de arquitectura de solución (commit `c255f1f`).
- Refactor de documentación SDD aplicando correcciones derivadas del análisis por subagentes (commit `1187572`).
- Revisión del flujo de desarrollo documentado (commit `f807dfb`).

### Deprecated

### Removed

### Fixed

### Security

---

## [1.0.2] - 2026-03-31

Release de mantenimiento de la línea 1.0. Corresponde al estado del MVP estabilizado tras la primera publicación pública de la Fase 1 (Sprints 01–04).

### Fixed

- Correcciones acumuladas sobre el pipeline DSL → AST → Evaluación → Render. Detalle completo disponible mediante `git log v1.0.1..v1.0.2`.

### Changed

- Ajustes menores sobre los renderers y la capa de validación derivados del feedback de integración end-to-end (`samples/MotorDsl.MultaApp.Nuget`).

---

## [1.0.1] - 2026-03-30

Release de patch sobre la línea 1.0. Estabilización de la primera publicación.

### Fixed

- Correcciones de defectos detectados inmediatamente después de la publicación 1.0.0. Detalle completo disponible mediante `git log v1.0.0..v1.0.1`.

---

## [1.0.0] - 2026-03-28

Primera release pública del Motor DSL. Cubre el alcance del MVP (Fase 1 — Sprints 01–04) definido en el roadmap de producto.

### Added

- Núcleo del Motor DSL (`MotorDsl.Core`): pipeline `DSL → Parseo → Validación → Evaluación → Render → Output`.
- Parser DSL (`MotorDsl.Parser`): construcción de AST a partir de plantillas DSL estructuradas.
- Capa de rendering (`MotorDsl.Rendering`): renderizador ESC/POS para impresión térmica.
- Capa de extensibilidad (`MotorDsl.Extensions`): puntos de extensión para nodos, funciones, evaluadores y renderers personalizados.
- Evaluador de expresiones y motor de reglas para resolución dinámica de nodos.
- Sistema de validación de plantillas DSL.
- Resolución de datos sobre contexto de ejecución.
- Motor de layout para composición de documentos.
- Contratos de entrada/salida estables para consumidores de la librería.
- Pipeline CI/CD con publicación automática a GitHub Packages disparada por tag `v*`.
- Documentación SDD completa: visión, alcance, roadmap, especificación funcional, arquitectura, backlog técnico, DoD/DoR y guía de integración.
- Aplicación de validación end-to-end `samples/MotorDsl.MultaApp.Nuget` consumiendo los cuatro paquetes desde el feed.
- Licencia MIT.

---

## Notas sobre la reconstrucción histórica

Este CHANGELOG fue inicializado de forma retroactiva. El repositorio no posee tags Git al momento de su creación; las versiones 1.0.0, 1.0.1 y 1.0.2 se reconstruyen tomando como autoridad la tabla de paquetes publicados en `docs/09_devops/entornos-deploy_v1.0.md` y el roadmap de producto. Las fechas históricas son aproximadas. A partir del primer tag Git formal, las entradas se generarán mirando `git log <tag-anterior>..<tag>` con commits Conventional Commits.

---

[Unreleased]: https://github.com/Aplicada-Streaming/Ejemplo_IA_SDD_Template/compare/v1.0.2...HEAD
[1.0.2]: https://github.com/Aplicada-Streaming/Ejemplo_IA_SDD_Template/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/Aplicada-Streaming/Ejemplo_IA_SDD_Template/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/Aplicada-Streaming/Ejemplo_IA_SDD_Template/releases/tag/v1.0.0
