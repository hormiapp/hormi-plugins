# Hormi para asistentes de IA

Hormi expone un servidor MCP en `https://api.hormi.app/mcp`. Cualquier cliente
compatible con MCP puede registrar gastos, responder cuanto gastaste y ordenar
categorias en tu hogar, despues de que inicies sesion una vez y apruebes los
permisos.

Este repositorio empaqueta esa conexion junto con las habilidades que le
ensenan al asistente las reglas del producto. El servidor es el mismo para
todos los clientes; lo unico que cambia es como cada uno lo instala.

## Como conectarlo

| Cliente | Como |
|---|---|
| Claude Code | `/plugin marketplace add hormiapp/hormi-plugins` y `/plugin install hormi@hormi` |
| Claude (web y escritorio) | Configuracion, Conectores, Anadir conector personalizado, y pega la URL |
| ChatGPT | Conector personalizado con la URL, si tu plan lo permite |
| Cursor | Anade la URL en su configuracion MCP |
| Codex | `codex mcp add hormi --url https://api.hormi.app/mcp` |
| Grok y otros | Cualquier cliente MCP con inicio de sesion acepta la URL |

Guia paso a paso por cliente: [hormi.app/docs/mcp](https://hormi.app/docs/mcp).

Solo el plugin de Claude Code esta verificado desde este repositorio. ChatGPT y
Grok no tienen un formato de plugin instalable para MCP: se conectan pegando la
URL o desde el directorio de conectores del proveedor, asi que no hay nada que
empaquetar aqui para ellos.

La primera herramienta que uses abre el inicio de sesion de Hormi y la pantalla
de permisos. En Claude Code, si no aparece, ejecuta `/mcp` y autoriza desde
ahi. Requiere Hormi Plus (los 14 dias de prueba cuentan).

## Que hay en este repositorio

| Ruta | Para quien |
|---|---|
| `.mcp.json` | Compartido: la URL del servidor y su transporte |
| `skills/` | Compartido: tres habilidades en formato Agent Skills |
| `.claude-plugin/plugin.json` | Claude Code |
| `.cursor-plugin/plugin.json` | Cursor |
| `.plugin/plugin.json` | Clientes que leen el manifiesto generico |
| `.claude-plugin/marketplace.json` | Claude Code exige el marketplace en la raiz del repositorio |

Los tres manifiestos declaran lo mismo y conviven como pares: ninguno es el
principal. Las habilidades solo las aprovechan los clientes que soportan Agent
Skills; el resto recibe igual las 16 herramientas y las instrucciones que el
servidor envia en `initialize`.

## Que puede hacer el asistente

- Registrar, corregir y borrar gastos e ingresos (solo los tuyos).
- Responder cuanto gastaron, en que categorias y quien, y leer el reporte
  mensual.
- Listar, crear, renombrar y borrar categorias (solo administradores).

No puede tocar tu cuenta, tu suscripcion ni los miembros del hogar: no existe
ningun permiso para eso. Los gastos privados de otros miembros nunca se ven.

Permisos que pide: `profile:read`, `expenses:read`, `expenses:write`,
`incomes:read`, `incomes:write`, `categories:read`, `categories:write`,
`households:read`, `reports:read`.

## Habilidades incluidas

| Habilidad | Cuando se activa |
|---|---|
| `registrar-gastos` | "registra 12.500 de supermercado", "corrige el gasto de ayer" |
| `resumen-de-gastos` | "cuanto gastamos este mes", "en que se nos fue la plata" |
| `categorias` | "que categorias tengo", "crea una categoria para mascotas" |

Copia mantenida en sincronia con `/.well-known/agent-skills/` en hormi.app.

## Actualizar y desinstalar

En Claude Code:

```
/plugin update hormi@hormi
/plugin uninstall hormi@hormi
```

En cualquier cliente, para revocar el acceso sin desinstalar nada, entra en
Hormi y quita la conexion desde la configuracion de aplicaciones conectadas.

## Soporte

support@hormi.app

---

## English

Hormi's MCP server lives at `https://api.hormi.app/mcp` and works with any
MCP client. This repository packages that connection plus three Agent Skills
that teach the assistant the product rules.

Claude Code installs it as a plugin:

```
/plugin marketplace add hormiapp/hormi-plugins
/plugin install hormi@hormi
```

Every other client connects with the URL. Per-client instructions:
[hormi.app/docs/mcp](https://hormi.app/docs/mcp). The manifests in
`.claude-plugin/`, `.cursor-plugin/` and `.plugin/` are peers and declare the
same plugin; the payload (`.mcp.json`, `skills/`) is shared. Requires Hormi
Plus (the 14-day trial counts).
