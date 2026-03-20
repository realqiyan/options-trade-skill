# 期权&策略查询工具

```typescript

  /**
   * 查询用户所有期权交易策略列表（List<OwnerStrategy>）。返回策略ID（strategyId）、名称、标的、扩展配置等（auto_trade为开启自动交易的策略）。
   *
   * @returns 返回对象包含：
   *   - data: 策略数组，每条数据包含：
   *     - strategyId: 策略唯一标识符
   *     - strategyName: 策略名称
   *     - strategyCode: 策略编码（如wheel_strategy、cc_strategy、default）
   *     - stage: 策略阶段（running=运行中、suspend=暂停）
   *     - startTime: 策略开始时间
   *     - code: 标的代码
   *     - lotSize: 每手数量
   *     - status: 策略状态（1=启用，0=禁用）
   *     - ext: 扩展配置Map（如auto_trade、target_delta等）
   */
  function queryAllStrategy();

  /**
   * 查询指定期权交易策略ID（OwnerStrategy.strategyId）的策略详细信息汇总和策略订单（List<OwnerOrder>）。返回策略汇总信息（包含期权策略（OwnerStrategy）、Delta、持股、盈利情况等关键指标）和订单（OwnerOrder）明细表格（包含标的代码、证券代码、类型、价格、数量、收益、费用、行权时间、交易时间、状态等详细信息等）。
   *
   * @param strategyId 策略ID（strategyId）
   * @returns 返回对象包含：
   *   - data: 策略信息
   *     - strategyId: 策略唯一标识符
   *     - strategyName: 策略名称
   *     - strategyCode: 策略编码
   *     - stage: 策略阶段
   *     - startTime: 策略开始时间
   *     - code: 标的代码
   *     - lotSize: 每手数量
   *     - status: 策略状态
   *     - ext: 扩展配置
   *   - summary: 策略汇总信息
   *     - strategyDelta: 策略总体Delta
   *     - optionsDelta: 策略总体Options Delta
   *     - optionsGamma: 策略总体Options Gamma
   *     - optionsTheta: 策略总体Options Theta
   *     - openOptionsQuantity: 策略未平仓的持有期权合约数
   *     - openOptionsCallQuantity: 策略未平仓的Call期权合约数
   *     - openOptionsPutQuantity: 策略未平仓的Put期权合约数
   *     - avgDelta: 策略平均每股Delta
   *     - totalFee: 总手续费
   *     - allOptionsIncome: 期权总收益(已扣除手续费)
   *     - allIncome: 策略所有交易总收益（包含股票和期权收益）
   *     - unrealizedOptionsIncome: 未实现期权收益
   *     - holdStockNum: 持有股票数
   *     - holdStockCost: 持有股票成本价
   *     - holdStockProfit: 持股盈亏
   *     - totalStockCost: 股票总成本
   *     - averageStockCost: 股票平均成本
   *     - currentStockPrice: 当前股价
   *     - putMarginOccupied: PUT订单保证金占用
   *   - orders: 订单数组，每条数据包含：
   *     - code: 证券代码
   *     - market: 市场代码
   *     - side: 订单方向（买入/卖出）
   *     - price: 交易价格
   *     - quantity: 交易数量
   *     - orderFee: 交易费用
   *     - tradeTime: 交易时间
   *     - strikeTime: 行权时间
   *     - status: 订单状态（已成交、已撤销、等待成交等）
   *     - groupId: 订单组ID（平台订单ID）
   *     - tradeFrom: 订单来源
   *     - subOrder: 是否为子订单
   *   - orderGroups: 订单分组Map，key为groupId，value包含：
   *     - totalIncome: 累计收益
   *     - totalOrderFee: 累计手续费
   *     - orderCount: 分组订单数
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
   * @returns 返回对象包含：
   *   - code: 股票代码
   *   - market: 市场代码
   *   - data: 到期日数组，每条数据包含：
   *     - strikeTime: 到期日（YYYY-MM-DD格式）
   *     - DTE: 距离到期日的天数
   *     - tag: 期权标签（月期权/周期权）
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
   * @returns 返回对象包含：
   *   - code: 股票代码
   *   - market: 市场代码
   *   - strikeTime: 到期日
   *   - DTE: 距离到期日的天数
   *   - data: 期权数据数组，每条数据包含：
   *     - code: 期权代码
   *     - market: 市场代码
   *     - delta: 希腊值Delta
   *     - gamma: 希腊值Gamma
   *     - theta: 希腊值Theta
   *     - vega: 希腊值Vega
   *     - rho: 希腊值Rho
   *     - impliedVolatility: 隐含波动率（百分比数值，如20表示20%）
   *     - premium: 溢价（百分比数值）
   *     - curPrice: 当前价格
   *     - openInterest: 未平仓数量
   *     - volume: 成交量
   *     - timeValue: 时间价值
   *     - intrinsicValue: 内在价值
   *     - sellAnnualYield: 卖出年化收益率（带%符号）
   *     - strikePriceDistance: 行权价距离现价涨跌幅（带%符号）
   */
  function queryOptionsChain(code: string, market: number, strikeDate: string, filterType: string, tradeType: string);

  /**
   * 查询期权买卖盘报价数据。期权期权买卖盘信息，包括不同价位的买卖挂单数量和价格。
   *
   * @param code 期权代码，如AAPL250620C150等
   * @param market 市场代码：1表示港股，11表示美股
   * @returns 返回对象包含：
   *   - data: 买卖盘数据
   *     - code: 期权代码
   *     - market: 市场代码
   *     - bidList: 买盘价格列表（按价格优先级排序）
   *     - askList: 卖盘价格列表（按价格优先级排序）
   */
  function queryOrderBook(code: string, market: number);

```
