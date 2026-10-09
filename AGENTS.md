# AGENTS.md

## Workflow de desarrollo con agentes (HITL)

Loop estándar: Diseño/Prompt (humano) → Generación de código (agente) → Checks
automatizados / PR → Code review humana → Merge. Detalle completo en
`CONTRIBUTING.md`. Reglas duras:

1. Trabajar siempre en feature branches cortas (`feature/xyz`, `fix/xyz`,
   `docs/xyz`); **nunca** commitear ni pushear directo a la rama principal.
2. Antes de pushear, correr tests y linters locales.
3. PRs chicos y focalizados (<200 líneas, un solo tema), con el template de
   `.github/PULL_REQUEST_TEMPLATE.md`: resumen, issue linkeado y evidencia de
   tests corridos (no alcanza con afirmar que funciona).
4. Declarar en el PR cuando el código fue generado por un agente.
5. Todo PR requiere revisión y aprobación humana + CI en verde antes del
   merge; el agente nunca mergea.
