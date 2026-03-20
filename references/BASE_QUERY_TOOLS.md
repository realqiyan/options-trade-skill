# 基础数据查询工具

```typescript
   /**
   * 查询股票实时价格。
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   * @returns 返回对象包含：
   *   - code: 股票代码
   *   - market: 市场代码
   *   - data: 股票价格数据
   */
  function queryStockRealPrice(code: string, market: number);

  /**
   * 查询股票K线数据（日K或周K）。返回结果包括指定数量的K线数据，每条K线包含日期、开盘价、收盘价、最高价、最低价、成交量和成交额。
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   * @param periodCode K线类型：1000表示日K线，2000表示周K线
   * @param count K线数量，最多可查询500条数据
   * @returns 返回对象包含：
   *   - code: 股票代码
   *   - market: 市场代码
   *   - period: K线类型名称（如"日K"、"周K"）
   *   - count: K线数量
   *   - data: K线数据数组，每条数据包含：
   *     - date: 日期（YYYY-MM-DD格式）
   *     - open: 开盘价
   *     - close: 收盘价
   *     - high: 最高价
   *     - low: 最低价
   *     - volume: 成交量
   *     - turnover: 成交额
   */
  function queryStockCandlesticks(code: string, market: number, periodCode: number, count: number);

  /**
   * 查询股票技术指标数据。返回结果包含指定数量的历史数据，每条数据包括日期、布林带下轨/中轨/上轨、EMA20/EMA5/EMA50指数移动平均线、MACD指标(DEA/DIF)、RSI相对强弱指数等。
   *
   * @param code 股票代码，如AAPL、TSLA等
   * @param market 市场代码：1表示港股，11表示美股
   * @param periodCode 指标周期：1000表示日线指标，2000表示周线指标
   * @param count 指标数量，最多可查询500条数据
   * @returns 返回对象包含：
   *   - code: 股票代码
   *   - market: 市场代码
   *   - period: 指标周期名称（如"日线"、"周线"）
   *   - count: 指标数量
   *   - data: 指标数据数组，每条数据包含：
   *     - date: 日期（YYYY-MM-DD格式）
   *     - BOLL_LOWER: 布林带下轨
   *     - BOLL_MIDDLE: 布林带中轨
   *     - BOLL_UPPER: 布林带上轨
   *     - EMA20: 20日指数移动平均线
   *     - EMA5: 5日指数移动平均线
   *     - EMA50: 50日指数移动平均线
   *     - MACD_DEA: MACD指标DEA线
   *     - MACD_DIF: MACD指标DIF线
   *     - RSI: RSI相对强弱指数
   *     - 其他技术指标...
   */
  function queryStockIndicator(code: string, market: number, periodCode: number, count: number);

  /**
   * 查询股票财报日历信息。包括财报日期、预期每股收益、实际每股收益(如已发布)等关键财务数据。
   *
   * @param code 股票代码，如AAPL、TSLA、BABA等
   * @returns 返回对象包含：
   *   - code: 股票代码
   *   - data: 财报日历数组，每条数据包含：
   *     - symbol: 股票代码
   *     - name: 公司名称
   *     - marketCap: 市值
   *     - fiscalQuarterEnding: 财报季度结束日期
   *     - epsForecast: 预期每股收益
   *     - noOfEsts: 分析师数量
   *     - lastYearRptDt: 去年财报发布日期
   *     - lastYearEps: 去年每股收益
   *     - time: 财报发布时间
   *     - earningsDate: 财报日期
   */
  function queryEarningsCalendar(code: string);

  /**
   * 查询用户所有持仓明细，包含股票和期权信息汇总，返回完整持仓表格，包含证券代码、证券名称、持仓数量（期权持仓数为负数表示卖出期权合约）、可卖数量、成本价、当前价等信息。**注意：整体持仓仅供参考，具体策略分析请使用`queryStrategyDetailAndOrders`查询策略执行明细。**
   *
   * @returns 返回对象包含：
   *   - data: 持仓数据数组，每条数据包含：
   *     - securityCode: 证券代码
   *     - market: 市场代码
   *     - securityName: 证券名称
   *     - quantity: 持仓数量（期权持仓数为负数表示卖出期权合约）
   *     - canSellQty: 可卖数量
   *     - costPrice: 成本价
   *     - currentPrice: 当前价
   *     - profit: 盈亏金额
   *     - profitRate: 盈亏比例
   */
  function queryAllPosition();


  /**
   * 查询VIX恐慌指数指标。返回结果包括当前VIX值，帮助投资者评估市场情绪和风险水平。
   *
   * @returns 返回对象包含：
   *   - data: 当前VIX值
   */
  function queryVixIndicator();
```
