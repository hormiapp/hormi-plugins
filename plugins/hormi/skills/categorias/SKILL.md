---
name: categorias
description: Keep a Hormi household's expense categories tidy - list, create, rename and delete categories through the Hormi MCP server, respecting the admin-only rule. Use when the user wants to see, add, rename or remove categories ("que categorias tengo", "crea una categoria para mascotas", "renombra Super a Supermercado").
---

# Category housekeeping in Hormi

Use this skill when the user wants to see, add, rename or remove expense
categories in Hormi. It needs the Hormi MCP server
(`https://api.hormi.app/mcp`) with the `categories:read` and
`categories:write` permissions.

## Rules

- Categories are shared by the whole household, so only household admins can
  create, edit or delete them. A `not_admin` error means the user should ask
  an admin; do not retry.
- Always call `list_categories` first. Suggest reusing an existing category
  before creating a near-duplicate ("Super" vs "Supermercado").
- `create_category(name, icon?, color?)`: names must be unique; the icon is a
  single emoji; the color a hex value like `#22C55E`.
- `update_category(category_id, name?, icon?, color?)` changes only the fields
  you pass. Existing expenses keep the category.
- `delete_category(category_id)` only works when no expenses use the
  category. If it fails with `validation_error`, offer to move those expenses
  with `update_expense` first, and confirm with the user before deleting.
