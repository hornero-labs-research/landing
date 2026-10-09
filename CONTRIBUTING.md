# Workflow de desarrollo con agentes de IA (HITL)

El workflow estándar, más efectivo y seguro para desarrollar software con agentes de IA es un loop **human-in-the-loop (HITL)**:

```
Diseño / Prompt → Generación de código por el agente → Checks automatizados / PR → Code review humana → Merge
```

La regla de oro: **el agente propone, el humano dispone**. Ningún código generado por IA llega a la rama principal sin revisión humana y CI en verde.

---

## El workflow estándar

### 1. Alcance y diseño (humano)

- **Definir boundaries claros:** partir las tareas en unidades chicas y aisladas (ej. "agregar tests unitarios para el módulo X", "fixear el bug Y en el archivo Z").
- **Dar contexto completo:** el agente debe tener acceso al contexto del proyecto, patrones de arquitectura y convenciones (`AGENTS.md`, este `CONTRIBUTING.md`, docs del repo).

### 2. Generación e iteración local (agente + humano)

- **Generar código en loops cortos:** el agente trabaja en una feature branch dedicada (`feature/xyz` o `fix/xyz`).
- **Correr tests y linters locales:** el agente ejecuta lint, formato y tests unitarios localmente **antes** de pushear.

### 3. Creación del Pull Request (agente)

El agente genera un PR (borrador) con detalles estructurados:

- Resumen de los cambios realizados.
- Issues linkeados (GitHub y/o Plane).
- Resultados de tests o logs que demuestren que funciona.
- Declaración de que el PR fue generado por un agente (cuál y con qué alcance).

Al abrirse el PR se dispara el pipeline de CI/CD: tests automatizados, análisis estático y scanners de seguridad.

### 4. Revisión humana y verificación (humano — paso crítico)

- **Revisar lógica y seguridad:** verificar edge cases, alineación con la arquitectura, vulnerabilidades potenciales y APIs alucinadas.
- **Feedback iterativo:** si hay problemas, dejar comentarios en el PR para que el agente los resuelva, o hacer ajustes rápidos a mano.

### 5. Merge y deploy (humano)

- **Aprobación final:** mergear solo cuando todos los status checks de CI/CD pasan y un revisor humano aprobó.
- El agente **nunca** mergea ni pushea directo a la rama principal.

---

## Buenas prácticas clave

| Fase | Hacer | Evitar |
| --- | --- | --- |
| **Branching** | Feature branches cortas y específicas por tarea. | Commitear directo a `main`/`master` o `develop`. |
| **Alcance del PR** | PRs chicos y focalizados (<200 líneas). | Mega-PRs con múltiples refactors no relacionados. |
| **Revisión** | Tratar el código de IA como el de un junior entusiasta: revisar lógica, tests y seguridad. | Mergear PRs en verde sin leer el código. |
| **Testing** | Exigir tests unitarios e integración automatizados en cada PR. | Confiar solo en el "el código funciona" del agente. |

---

## Notas específicas de este repo

- Las reglas operativas que los agentes leen automáticamente están en `AGENTS.md`.
- Stack: sitio HTML estático (repo público).
