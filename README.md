# thefinancial.ai

![thefinancial.ai](./assets/logo.png)

**Financial AI® — Research, Forecasts & Strategy Backtesting**

Bring Financial AI’s investment intelligence directly into Claude. Explore company research, proprietary financial and macroeconomic forecasts, and strategy backtesting through natural conversation. The platform incorporates a comprehensive set of technical, economic, and valuation indicators and enables strategies across equities, ETFs, options, futures, cryptocurrencies, and other asset classes, tailored to specific user requirements and investment objectives.

### What you can do

- **Research investments:** Analyze companies, sectors, and market developments.
- **Look ahead:** Explore company financial forecasts and macroeconomic projections.
- **Test ideas:** Build and backtest investment strategies before putting capital to work.

### Try asking

- “Based on Financial AI’s forecasts, do you think AMD will deliver upside surprise?”
- “Based on the current momentum of MU, provide an otm put option list on MU up to 60 days to expiration for a $200 to $1500 credit with minimal assignment risk”
- “Backtest buying NASDAQ futures when bar close price is below its 20 period moving average on 1 min bars, and on 10 min bars, its 5 period moving average is below its 20 period moving average with 0 bp transaction cost”

This plugin connects Claude to [thefinancial.ai](https://thefinancial.ai)'s MCP server.

thefinancial.ai provides information and analysis, not personal investment advice. This plugin cannot place
orders or move money.

## What's in the plugin

| Component | What it does |
| --- | --- |
| `thefinancial-ai` MCP connector (`.mcp.json`) | Connects to thefinancial.ai's remote MCP server at `https://thefinancial.ai/api/finai-mcp`. All tools run on thefinancial.ai's servers. |
| `thefinancial-ai` skill (`skills/financial-ai/SKILL.md`) | Tells Claude which tool fits which request, how to wait for long analyses, and how to present the results and charts. |

The plugin contains no local code: nothing is installed or run on your computer.

## Requirements

- A thefinancial.ai account. Create one at [thefinancial.ai](https://thefinancial.ai).
- Claude (web, desktop or mobile), Cowork or Claude Code.

## Connect

1. Install the plugin from the directory.
2. Open the plugin's **Connectors** tab and connect **thefinancial-ai**.
3. Claude opens thefinancial.ai's sign-in page. Sign in with your thefinancial.ai email and password (or
   click **Allow** if you are already signed in to the website in that browser).

The connection uses OAuth 2.1: Claude never sees your password, and the access it gets is limited to
your own thefinancial.ai account. You can disconnect at any time from Claude's connector settings.

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
| `search_functions`, `describe_functions` | No | Find thefinancial.ai data functions (prices, fundamentals, estimates, indicators, macro series, options, ETF holdings) and read their documentation. |
| `call_function` | No | Fetches data from one function and returns a compact summary plus a handle to the full result. |
| `get_result` | No | Pages through a stored result. Results are kept for 24 hours. |
| `run_python` | No | Runs a Python analysis (pandas, numpy) in thefinancial.ai's isolated sandbox, next to the data, and returns only the answer. |
| `list_skills`, `get_skill` | No | Load step-by-step workflows for research, screening, backtesting, options, macro and portfolio reviews. |
| `call_write_function` | **Yes** | Changes your thefinancial.ai account: manual portfolios, watchlist, saved strategies and screeners, notification settings. Claude asks for your confirmation before each call. |

Long analyses (backtests, multi-strategy comparisons) can take several minutes. The tools return a
progress handle while they run, and Claude collects the result when it is ready.

## Data and privacy

- **What is sent:** the questions you ask through these tools and the arguments of each tool call. The
  plugin does not read your conversation history, your files or Claude's memory.
- **Where it goes:** only to thefinancial.ai (`https://thefinancial.ai`). thefinancial.ai processes your
  request with its own AI agent and data services, as described in its
  [privacy policy](https://thefinancial.ai/privacy-policy).
- **What is stored:** tool results are kept on thefinancial.ai's servers for 24 hours so they can be paged
  and downloaded. Changes you make with `call_write_function` are saved to your thefinancial.ai account.
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
[MIT License](./LICENSE). Use of the thefinancial.ai service is governed by its
[terms and conditions](https://thefinancial.ai/terms-and-conditions).
