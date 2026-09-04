---
name: registrar-gastos
description: Record, correct and delete household expenses and incomes in Hormi through its MCP server, the way a careful assistant would - confirm amounts, pick existing categories, respect privacy. Use when the user asks to log, fix or remove an expense or income ("registra 12.500 de supermercado", "anota el alquiler", "corrige el gasto de ayer", "borra el cafe duplicado", "log this expense").
---

# Record expenses and incomes in Hormi

Use this skill when the user asks to log, fix or remove an expense or income in
Hormi. It needs the Hormi MCP server (`https://api.hormi.app/mcp`) connected
with the `expenses:write` and, for incomes, `incomes:write` permissions. Hormi
MCP access is a Plus feature; if a tool fails with `subscription_required`,
tell the user to activate Hormi Plus.

## Before writing

1. Call `get_profile` once per conversation: answer in the user's language and
   use their household's currency. Never convert currencies.
2. When the category is unclear, call `list_categories` and pick the closest
   existing name; do not invent one. Only household admins can create
   categories (`create_category` fails with `not_admin` otherwise).
3. Confirm with the user when the amount or description is ambiguous, for
   example a message that mentions two numbers.

## Recording

- `add_expense(amount, description, category?, expense_date?, is_private?)`.
  Dates are `YYYY-MM-DD` in the user's time zone; omit for today.
- Mark `is_private: true` only when the user says the expense is personal
  ("privado", "mio", "que no lo vean").
- `add_income` works the same way and needs income tracking enabled for the
  household (`incomes_disabled` otherwise).

## Correcting and deleting

- Find the record with `list_expenses` or `list_incomes` (newest first) and
  use its `id`. Only records with `is_yours: true` can be changed; other
  members' records return `not_owner`.
- `update_expense` / `update_income` change only the fields you pass.
- Before `delete_expense` or `delete_income`, show the record (date,
  description, amount) and get an explicit yes. Deletions cannot be undone
  through the connection.

## Answering

Report what was recorded in one line: date, description, amount with currency,
category. Suggest nothing else unless asked.
