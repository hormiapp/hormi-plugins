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
| Grok Build | Marketplace de xAI (envio pendiente); mientras tanto, la URL |
| Otros | Cualquier cliente MCP con inicio de sesion acepta la URL |

Guia paso a paso por cliente: [hormi.app/docs/mcp](https://hormi.app/docs/mcp).

Solo el plugin de Claude Code esta verificado desde este repositorio. ChatGPT
tiene su propio camino: OpenAI publica plugins desde su portal, donde se envia
el endpoint del servidor y las habilidades, no un manifiesto alojado en un
repositorio. Por eso ahi no hay nada que empaquetar aqui, aunque el plugin si
exista. Grok Build instala plugins desde el marketplace de xAI, que usa este mismo
formato: el envio de Hormi esta pendiente de revision. Mientras tanto, y en
cualquier otro cliente MCP, la URL funciona.

La primera herramienta que uses abre el inicio de sesion de Hormi y la pantalla
de permisos. En Claude Code, si no aparece, ejecuta `/mcp` y autoriza desde
ahi. Requiere Hormi Plus (los 14 dias de prueba cuentan).

## Que hay en este repositorio

| Ruta | Para quien |
|---|---|
| `.mcp.json` | Compartido: la URL del servidor y su transporte |
| `skills/` | Compartido: tres habilidades en formato Agent Skills |
| `.claude-plugin/plugin.json` | Claude Code |
| `.grok-plugin/plugin.json` | Grok Build |
| `.cursor-plugin/plugin.json` | Cursor |
| `.plugin/plugin.json` | Clientes que leen el manifiesto generico |
| `.claude-plugin/marketplace.json` | Claude Code exige el marketplace en la raiz del repositorio |

Los tres manifiestos declaran lo mismo y conviven como pares: ninguno es el
principal. Las habilidades solo las aprovechan los clientes que soportan Agent
Skills; el resto recibe igual las 16 herramientas y las instrucciones que el
servidor envia en `initialize`.

## Red y credenciales

Declaracion para quien revise este plugin:

- **Un solo endpoint.** El plugin habla unicamente con
  `https://api.hormi.app/mcp` sobre HTTPS. No hay ninguna otra llamada de red.
- **Sin secretos en el repositorio.** La autenticacion es OAuth 2.1 con PKCE:
  el token lo emite `api.hormi.app` y lo guarda el cliente MCP. Aqui no hay
  claves, tokens ni credenciales.
- **Sin ejecucion de codigo local.** No hay hooks, comandos, agentes, binarios,
  dependencias ni scripts de instalacion. El paquete son archivos Markdown y
  dos JSON de configuracion.
- **Telemetria.** El plugin no envia nada por su cuenta. El servidor si registra
  el uso de herramientas en la cuenta Hormi del usuario, como el resto del
  producto.

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

The plugin talks to `https://api.hormi.app/mcp` and nothing else, over OAuth
2.1; it ships no executable code, no hooks and no credentials.

Every other client connects with the URL. Per-client instructions:
[hormi.app/docs/mcp](https://hormi.app/docs/mcp). The manifests in
`.claude-plugin/`, `.cursor-plugin/` and `.plugin/` are peers and declare the
same plugin; the payload (`.mcp.json`, `skills/`) is shared. Requires Hormi
Plus (the 14-day trial counts).
