---
name: financial-ai
description: Use for questions about stocks, ETFs, indices, crypto, company financials (revenue, earnings, EBITDA, margins, segments), prices, returns, technical indicators, forecasts and analyst estimates, options, macro data, stock screens, trading-strategy backtests, or the user's own Financial.AI portfolios and watchlist. Explains which financial.ai tool fits the request, how to wait for long analyses, and how to present the results and charts.
---

# financial.ai

financial.ai is Financial.AI's connector: a financial AI with licensed market data and its own
analytics (prices and technicals, fundamentals, forecasts, screening, backtests, options and portfolio
analysis). It works through the tools of the `financial-ai` MCP server (`ask_financial_ai`,
`search_functions`, `call_function`, `list_skills`, …).

Prices, financials and estimates change daily, so figures in your answer should come from these tools
rather than from memory.

If none of these tools are available, the connector isn't connected yet: tell the user to connect
**financial-ai** in the plugin's Connectors tab and sign in with their Financial.AI account.

## Pick the tool

| The user wants | Use |
| --- | --- |
| An answer or an analysis — most questions ("AAPL revenue", "is NVDA overbought?", "backtest …", "screen for …") | `ask_financial_ai(question)`, or the focused tool for that kind of question (`get_company_financials`, `get_stock_price_data`, `screen_stocks`, `backtest_strategy`, `get_market_forecast`) |
| Specific raw data to work with (a price series, a fundamentals table) | `search_functions` → `describe_functions` → `call_function` → `get_result` |
| Several data pulls plus real computation (returns, correlations, a custom rule) | `run_python`, with `sdk.<Function>(...)` inside |
| Something in their own account (portfolios, watchlist, saved strategies) | `call_function` to read, `call_write_function` to change |
| A chart | draw it from the answer's ```` ```chart ```` blocks — `get_skill("charting")` |
| A step-by-step workflow for a bigger task | `list_skills`, then `get_skill(name)` |

## ask_financial_ai and the focused tools

- Pass the user's question **verbatim**. Don't rewrite it into a spec and don't add date ranges or
  assumptions: the agent picks sensible defaults and says which ones it used.
- Most answers take 30 s–3 min; backtests and multi-strategy comparisons can take 10+ minutes. While
  the result says `status: "in_progress"`, wait `retry_after_seconds` and call the same tool again with
  only `{"job": "<job>"}`. Don't re-ask the question to check on it.
- A `finished` answer is complete (text, tables, and for each chart a data summary plus a
  ```` ```chart ```` block). Present it; don't call again to verify or recompute its figures. When a
  chart helps, draw it from its block.
- The tools are stateless: put everything needed in the question ("…for the portfolio AAPL 40%,
  MSFT 60%").
- If the answer ends with an `answer_id` and the user wants to keep the strategy or screen, call
  `call_write_function` with `save_strategy_from_answer` or `save_screener_from_answer`.

## Skills (detailed workflows)

Call `list_skills` for the current list, then `get_skill(name)` for the one that fits. Load one before a
multi-step task: company research, backtests, screens, options, macro, portfolio reviews, custom Python
analysis. Each skill says which tools to call, in what order, and what the defaults and pitfalls are.

## Rules

- Say where numbers come from ("Financial.AI") and give their as-of date.
- If a tool returns no data, say so instead of filling the gap from memory.
- Account tools act on the signed-in user's own data only. Ask before anything that deletes or
  overwrites. No orders can be placed through Financial.AI.
- Results from `call_function` / `run_python` stay on the server: page them with `get_result`, or give
  the user the CSV/JSON download link.
- Financial.AI provides information and analysis, not personal investment advice.
