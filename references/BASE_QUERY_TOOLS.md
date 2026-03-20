# 基础数据查询工具

```typescript
   /**
   * 查询股票实时价格。
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   */
  function queryStockRealPrice(code: string, market: number);

  /**
   * 查询股票K线数据（日K或周K）。返回结果包括指定数量的K线数据，每条K线包含日期、开盘价、收盘价、最高价、最低价、成交量和成交额。
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   * @param periodCode K线类型：1000表示日K线，2000表示周K线
   * @param count K线数量，最多可查询500条数据
   */
  function queryStockCandlesticks(code: string, market: number, periodCode: number, count: number);

  /**
   * 查询股票技术指标数据。返回结果包含指定数量的历史数据，每条数据包括日期、布林带下轨/中轨/上轨、EMA20/EMA5/EMA50指数移动平均线、MACD指标(DEA/DIF)、RSI相对强弱指数等。
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   * @param periodCode 指标周期：1000表示日线指标，2000表示周线指标
   * @param count 指标数量，最多可查询500条数据
   */
  function queryStockIndicator(code: string, market: number, periodCode: number, count: number);

  /**
   * 查询股票财报日历信息。包括财报日期、预期每股收益、实际每股收益(如已发布)等关键财务数据。
   *
   * @param code 股票代码，如AAPL、TSLA、BABA等
   */
  function queryEarningsCalendar(code: string);

  /**
   * 查询用户所有持仓明细，包含股票和期权信息汇总，返回完整持仓表格，包含证券代码、证券名称、持仓数量（期权持仓数为负数表示卖出期权合约）、可卖数量、成本价、当前价等信息。**注意：整体持仓仅供参考，具体策略分析请使用`queryStrategyDetailAndOrders`查询策略执行明细。**
   */
  function queryAllPosition();


  /**
   * 查询VIX恐慌指数指标。返回结果包括当前VIX值，帮助投资者评估市场情绪和风险水平。
   */
  function queryVixIndicator();
```
