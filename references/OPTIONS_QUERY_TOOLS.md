# 期权&策略查询工具

```typescript

  /**
   * 查询用户所有期权交易策略列表（List<OwnerStrategy>）。返回策略ID（strategyId）、名称、标的、扩展配置等（auto_trade为开启自动交易的策略）。
   */
  function queryAllStrategy();

  /**
   * 查询指定期权交易策略ID（OwnerStrategy.strategyId）的策略详细信息汇总和策略订单（List<OwnerOrder>）。返回策略汇总信息（包含期权策略（OwnerStrategy）、Delta、持股、盈利情况等关键指标）和订单（OwnerOrder）明细表格（包含标的代码、证券代码、类型、价格、数量、收益、费用、行权时间、交易时间、状态等详细信息等）。
   *
   * @param strategyId 策略ID（strategyId）
   */
  function queryStrategyDetailAndOrders(strategyId: string);

  /**
   * 查询期权交易策略规则。策略规则包含具体的交易规则、delta要求、行权日期选择要求、技术指标要求等详细信息。
   *
   * @param strategyCode? 期权策略编码，可选值：cc_strategy(备兑看涨策略)、wheel_strategy(车轮策略)、default(默认卖期权策略)，不指定时返回所有策略。
   */
  function queryStrategyRule(strategyCode?: string);

  /**
   * 查询指定股票的期权近10个到期日列表，返回到期日列表包含：到期日(strikeTime)、DTE、月期权｜周期权
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   */
  function queryOptionsExpDate(code: string, market: number);

  /**
   * 查询期权链详细信息，使用前请先使用queryOptionsExpDate工具获取有效的到期日。返回结果包括期权代码、类型(Call/Put)、行权价、当前价格、隐含波动率、希腊字母(Delta、Theta、Gamma)、未平仓合约数、当天交易量等完整信息。
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   * @param strikeDate 期权到期日，格式为YYYY-MM-DD，如2025-06-27。请先使用queryOptionsExpDate工具获取有效日期
   * @param filterType 期权类型过滤：ALL(全部期权)、PUT(看跌期权)或CALL(看涨期权)
   * @param tradeType 交易类型：SELL(卖出)或BUY(买入)。
   */
  function queryOptionsChain(code: string, market: number, strikeDate: string, filterType: string, tradeType: string);

  /**
   * 查询期权买卖盘报价数据。期权期权买卖盘信息，包括不同价位的买卖挂单数量和价格。
   *
   * @param code 期权代码，如AAPL250620C150等
   * @param market 市场代码：1表示港股，11表示美股
   */
  function queryOrderBook(code: string, market: number);

```
