# financial.ai

![financial.ai](./assets/logo.png)

financial.ai connects Claude to [Financial.AI](https://thefinancial.ai), a financial AI with licensed
market data and its own analytics. Ask about stocks, ETFs, indices and crypto in plain words and get
answers computed from Financial.AI's data: company financials, prices and technical indicators,
forecasts and analyst estimates, earnings, stock screens, trading-strategy backtests, options and macro
data. With your Financial.AI account connected, Claude can also read and update your own portfolios,
watchlist and saved strategies.

Financial.AI provides information and analysis, not personal investment advice. It cannot place
orders or move money.

## What's in the plugin

| Component | What it does |
| --- | --- |
| `financial-ai` MCP connector (`.mcp.json`) | Connects to Financial.AI's remote MCP server at `https://thefinancial.ai/api/finai-mcp`. All tools run on Financial.AI's servers. |
| `financial-ai` skill (`skills/financial-ai/SKILL.md`) | Tells Claude which tool fits which request, how to wait for long analyses, and how to present the results and charts. |

The plugin contains no local code: nothing is installed or run on your computer.

## Requirements

- A Financial.AI account. Create one at [Financial.AI](https://thefinancial.ai).
- Claude (web, desktop or mobile), Cowork or Claude Code.

## Connect

1. Install the plugin from the directory.
2. Open the plugin's **Connectors** tab and connect **financial-ai**.
3. Claude opens Financial.AI's sign-in page. Sign in with your Financial.AI email and password (or
   click **Allow** if you are already signed in to the website in that browser).

The connection uses OAuth 2.1: Claude never sees your password, and the access it gets is limited to
your own Financial.AI account. You can disconnect at any time from Claude's connector settings.

## Try it

- "What was Apple's revenue by segment over the last four quarters?"
- "Is NVDA overbought? Show RSI and the 50/200-day moving averages."
- "Backtest a 50/200-day golden cross on SPY over the last 5 years against buy and hold."
- "Which S&P 500 stocks have a P/E below 15 and revenue growth above 10%?"
- "When does Microsoft report earnings next, and what is the consensus EPS?"
- "How is my Core Growth portfolio doing this month?"
- "Add AMD to my watchlist."

## Tools

| Tool | Changes your account? | What it does |
| --- | --- | --- |
| `ask_financial_ai` | No | Answers any financial question with a finished analysis: text, tables and the data behind each chart. |
| `get_company_financials`, `get_stock_price_data`, `screen_stocks`, `backtest_strategy`, `get_market_forecast` | No | The same analysis, focused on one kind of question. |
| `search_functions`, `describe_functions` | No | Find Financial.AI data functions (prices, fundamentals, estimates, indicators, macro series, options, ETF holdings) and read their documentation. |
| `call_function` | No | Fetches data from one function and returns a compact summary plus a handle to the full result. |
| `get_result` | No | Pages through a stored result. Results are kept for 24 hours. |
| `run_python` | No | Runs a Python analysis (pandas, numpy) in Financial.AI's isolated sandbox, next to the data, and returns only the answer. |
| `list_skills`, `get_skill` | No | Load step-by-step workflows for research, screening, backtesting, options, macro and portfolio reviews. |
| `call_write_function` | **Yes** | Changes your Financial.AI account: manual portfolios, watchlist, saved strategies and screeners, notification settings. Claude asks for your confirmation before each call. |

Long analyses (backtests, multi-strategy comparisons) can take several minutes. The tools return a
progress handle while they run, and Claude collects the result when it is ready.

## Data and privacy

- **What is sent:** the questions you ask through these tools and the arguments of each tool call. The
  plugin does not read your conversation history, your files or Claude's memory.
- **Where it goes:** only to Financial.AI (`https://thefinancial.ai`). Financial.AI processes your
  request with its own AI agent and data services, as described in its
  [privacy policy](https://thefinancial.ai/privacy-policy).
- **What is stored:** tool results are kept on Financial.AI's servers for 24 hours so they can be paged
  and downloaded. Changes you make with `call_write_function` are saved to your Financial.AI account.
- **Downloads:** some results include a CSV or JSON download link. The link is signed, expires, and is
  the only credential needed to open it, so share it only with people who may see that data.

## Limits

- Each connection can make about 120 tool calls a minute and start about 30 full analyses an hour.
- Market data is current to the latest close; intraday data is available for backtests of intraday rules.
- No trading: orders cannot be placed and money cannot be moved through this plugin.

## Support

- Help and questions: [thefinancial.ai/contact](https://thefinancial.ai/contact) or
  [support@thefinancial.ai](mailto:support@thefinancial.ai)
- [Terms and conditions](https://thefinancial.ai/terms-and-conditions) ·
  [Privacy policy](https://thefinancial.ai/privacy-policy) ·
  [Disclaimers and disclosures](https://thefinancial.ai/disclaimers-and-disclosures)

## License

The plugin files in this repository (manifest, skill and documentation) are released under the
[MIT License](./LICENSE). Use of the Financial.AI service is governed by its
[terms and conditions](https://thefinancial.ai/terms-and-conditions).
