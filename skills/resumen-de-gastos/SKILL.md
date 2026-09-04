---
name: resumen-de-gastos
description: Answer questions about a household's spending in Hormi - totals, category and member breakdowns, balances and the monthly report - using the Hormi MCP server. Use when the user asks how much was spent, where the money went, how this month compares, or what the monthly report says ("cuanto gastamos este mes", "en que se nos fue la plata", "how much did we spend on groceries").
---

# Spending summaries from Hormi

Use this skill when the user asks how much they or their household spent,
where the money went, how this month compares, or what the monthly report
says. It needs the Hormi MCP server (`https://api.hormi.app/mcp`) with the
`expenses:read` permission (`incomes:read` for balances, `reports:read` for
the monthly report).

## Which tool

- `get_spending_summary(start_date?, end_date?)`: total, daily average,
  breakdown by category and by member. Defaults to the current month. When the
  household tracks incomes it also returns `total_incomes` and `balance`
  (incomes minus expenses; positive means the household saved money).
- `list_expenses(start_date?, end_date?, category?, limit?)`: the individual
  records, newest first. Use it for "what did we spend on X" questions and to
  find ids for corrections. `total_listed` covers only the returned rows; when
  `truncated` is true, use the summary for totals.
- `get_latest_report`: the household's most recent monthly report (a
  card-based summary Hormi generates at the start of each month).
  `has_report: false` is normal for new households.

## Rules

- Dates are `YYYY-MM-DD` in the user's time zone. "Este mes" means from the
  first of the month to today; "el mes pasado" is the full previous month.
- Amounts are already in the household's currency (see `get_profile` or
  `get_household`); format them the way the user's locale does and never
  convert.
- Other members' private expenses are not included and cannot be requested.
- Keep answers short: the headline number first, then at most the top three
  categories. Offer the full breakdown only if the user wants it.
