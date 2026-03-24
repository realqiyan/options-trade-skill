# 基础数据查询工具

```typescript

/**
 * 查询股票实时价格。
 * //returns 返回对象包含：
 * // - code: 股票代码
 * // - market: 市场代码
 * // - data: 股票实时价格数据
 *
 * @param code 股票代码，如AAPL、TSLA等
 * @param market 市场代码：1(港股)|11(美股)
 */
function queryStockRealPrice(code: string, market: number);

/**
 * 查询期权实时数据。
 * //returns 返回对象包含：
 * // - data: 期权实时数据
 * // -- code: 期权代码
 * // -- market: 市场代码
 * // -- delta: 希腊值Delta
 * // -- gamma: 希腊值Gamma
 * // -- theta: 希腊值Theta
 * // -- vega: 希腊值Vega
 * // -- rho: 希腊值Rho
 * // -- impliedVolatility: 隐含波动率
 * // -- curPrice: 当前价格
 * // -- openInterest: 未平仓数量
 * // -- volume: 成交量
 * // -- timeValue: 时间价值
 * // -- intrinsicValue: 内在价值
 *
 * @param code 期权代码，如AAPL250620C150等
 * @param market 市场代码：1(港股)|11(美股)
 */
function queryOptionsRealtimeData(code: string, market: number);

/**
 * 查询股票K线数据。
 * //returns 返回对象包含：
 * // - code: 股票代码
 * // - market: 市场代码
 * // - period: K线类型名称
 * // - count: K线数量
 * // - data: K线数据数组，每条数据包含：
 * // -- date: 日期（YYYY-MM-DD格式）
 * // -- open: 开盘价
 * // -- close: 收盘价
 * // -- high: 最高价
 * // -- low: 最低价
 * // -- volume: 成交量
 * // -- turnover: 成交额
 *
 * @param code 股票代码，如AAPL、TSLA等
 * @param market 市场代码：1(港股)|11(美股)
 * @param periodCode K线类型：DAY|WEEK
 * @param count K线数量，最多可查询500条数据
 */
function queryStockCandlesticks(code: string, market: number, periodCode: string, count: number);

/**
 * 查询股票技术指标。
 * //returns 返回对象包含：
 * // - code: 股票代码
 * // - market: 市场代码
 * // - period: 指标周期名称
 * // - count: 指标数量
 * // - data: 技术指标数据数组
 * // -- date: 日期（YYYY-MM-DD格式）
 * // -- BOLL_LOWER: 布林带下轨
 * // -- BOLL_MIDDLE: 布林带中轨
 * // -- BOLL_UPPER: 布林带上轨
 * // -- EMA20: 20日指数移动平均线
 * // -- EMA5: 5日指数移动平均线
 * // -- EMA50: 50日指数移动平均线
 * // -- MACD_DEA: MACD指标DEA线
 * // -- MACD_DIF: MACD指标DIF线
 * // -- RSI: RSI相对强弱指数
 * // -- 其他技术指标...
 *
 * @param code 股票代码，如AAPL、TSLA等
 * @param market 市场代码：1(港股)|11(美股)
 * @param periodCode 指标周期：DAY|WEEK
 * @param count 指标数量，最多可查询500条数据
 */
function queryStockIndicator(code: string, market: number, periodCode: string, count: number);

/**
 * 查询股票财报日历信息。
 * //returns 返回对象包含：
 * // - code: 股票代码
 * // - data: 财报日历数组，每条数据包含：
 * // -- symbol: 股票代码
 * // -- name: 公司名称
 * // -- marketCap: 市值
 * // -- fiscalQuarterEnding: 财报季度结束日期
 * // -- epsForecast: 预期每股收益
 * // -- noOfEsts: 分析师数量
 * // -- lastYearRptDt: 去年财报发布日期
 * // -- lastYearEps: 去年每股收益
 * // -- time: 财报发布时间
 * // -- earningsDate: 财报日期
 *
 * @param code 股票代码，如AAPL、TSLA、BABA等
 */
function queryEarningsCalendar(code: string);

/**
 * 查询用户所有持仓明细，包含股票和期权信息汇总。**注意：整体持仓仅供参考，具体策略分析请使用`queryStrategyDetailAndOrders`查询策略执行明细。**
 * //returns 返回对象包含：
 * // - data: 持仓数组，每条数据包含：
 * // -- code: 证券代码
 * // -- market: 市场代码
 * // -- quantity: 持仓数量
 * // -- availableQuantity: 可用数量
 * // -- costPrice: 成本价
 * // -- marketPrice: 市场价
 * // -- profit: 盈亏
 * // -- profitRate: 盈亏比例
 */
function queryAllPosition();

/**
 * 查询VIX恐慌指数指标。
 * //returns 返回对象包含：
 * // - data: VIX指数当前值
 */
function queryVixIndicator();
```
