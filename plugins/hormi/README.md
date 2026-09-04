# hormi

Conecta Claude Code con tu hogar de Hormi.

```
/plugin marketplace add hormiapp/hormi-plugins
/plugin install hormi@hormi
```

## Que puede hacer el asistente

- Registrar, corregir y borrar gastos e ingresos (solo los tuyos).
- Responder cuanto gastaron, en que categorias y quien, y leer el reporte
  mensual.
- Listar, crear, renombrar y borrar categorias (solo administradores).

No puede tocar tu cuenta, tu suscripcion ni los miembros del hogar: no existe
ningun permiso para eso. Los gastos privados de otros miembros nunca se ven.

## Permisos que pide

`profile:read`, `expenses:read`, `expenses:write`, `incomes:read`,
`incomes:write`, `categories:read`, `categories:write`, `households:read`,
`reports:read`. Los apruebas una vez en la pantalla de consentimiento de
Hormi.

## Requisitos

Hormi Plus activo (los 14 dias de prueba cuentan). Sin plan, las herramientas
responden `subscription_required`.

## Habilidades incluidas

| Habilidad | Cuando se activa |
|---|---|
| `registrar-gastos` | "registra 12.500 de supermercado", "corrige el gasto de ayer" |
| `resumen-de-gastos` | "cuanto gastamos este mes", "en que se nos fue la plata" |
| `categorias` | "que categorias tengo", "crea una categoria para mascotas" |

Copia mantenida en sincronia con `/.well-known/agent-skills/` en hormi.app.

## Soporte

support@hormi.app - [hormi.app/docs/mcp](https://hormi.app/docs/mcp)
