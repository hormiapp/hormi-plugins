# Hormi plugins

Marketplace oficial de Hormi para Claude Code. Instala el plugin `hormi` y tu
asistente puede registrar gastos, responder cuanto gastaste y ordenar
categorias en tu hogar de Hormi, sin pegar ninguna URL.

## Instalacion

```
/plugin marketplace add hormiapp/hormi-plugins
/plugin install hormi@hormi
```

La primera herramienta que uses abre el inicio de sesion de Hormi y la
pantalla de permisos. Si no aparece, ejecuta `/mcp` dentro de Claude Code y
autoriza Hormi desde ahi.

Requiere Hormi Plus (los 14 dias de prueba cuentan).

## Que incluye

| Componente | Detalle |
|---|---|
| Servidor MCP | `https://api.hormi.app/mcp`, transporte HTTP, OAuth 2.1 con pantalla de consentimiento |
| Habilidades | `registrar-gastos`, `resumen-de-gastos`, `categorias`: le ensenan al asistente las reglas del producto antes de que llame a una herramienta |

Las 16 herramientas y los permisos que pide cada una estan documentados en
[hormi.app/docs/mcp](https://hormi.app/docs/mcp).

## Actualizar y desinstalar

```
/plugin update hormi@hormi
/plugin uninstall hormi@hormi
```

Para revocar el acceso sin desinstalar, entra en Hormi y quita la conexion
desde la configuracion de aplicaciones conectadas.

## Otros clientes

Claude (web y escritorio), Codex, Cursor y cualquier cliente MCP con inicio de
sesion: la guia por cliente esta en
[hormi.app/docs/mcp](https://hormi.app/docs/mcp).

## Soporte

support@hormi.app

---

## English

Official Hormi marketplace for Claude Code. Install the `hormi` plugin and your
assistant can record expenses, answer spending questions and manage categories
in your Hormi household.

```
/plugin marketplace add hormiapp/hormi-plugins
/plugin install hormi@hormi
```

The first tool call opens the Hormi login and consent screen; run `/mcp` to
authorize manually. Requires Hormi Plus (the 14-day trial counts). Full
documentation: [hormi.app/docs/mcp](https://hormi.app/docs/mcp).
