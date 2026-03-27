# 期权&策略查询工具

```typescript
/**
 * 查询用户所有期权交易策略列表。
 * //returns 返回对象包含：
 * // - data: 策略数组，每条数据包含：
 * // -- strategyId: 策略唯一标识符
 * // -- strategyName: 策略名称
 * // -- strategyCode: 策略编码（如wheel_strategy、cc_strategy、default）
 * // -- stage: 策略阶段（running=运行中、suspend=暂停）
 * // -- startTime: 策略开始时间
 * // -- code: 标的代码
 * // -- lotSize: 每手数量
 * // -- status: 策略状态（1=启用，0=禁用）
 * // -- ext: 扩展配置Map（如auto_trade、target_delta等）
 */
function queryAllStrategy();

/**
 * 基于策略ID查询指定期权交易策略详细信息和当前有效订单。
 * //returns 返回对象包含：
 * // - data: 策略信息
 * // -- strategyId: 策略唯一标识符
 * // -- strategyName: 策略名称
 * // -- strategyCode: 策略编码
 * // -- stage: 策略阶段
 * // -- startTime: 策略开始时间
 * // -- code: 标的代码
 * // -- lotSize: 每手数量
 * // -- status: 策略状态
 * // -- ext: 扩展配置
 * // - summary: 策略汇总信息
 * // -- strategyDelta: 策略总体Delta
 * // -- optionsDelta: 策略总体Options Delta
 * // -- optionsGamma: 策略总体Options Gamma
 * // -- optionsTheta: 策略总体Options Theta
 * // -- openOptionsQuantity: 策略未平仓的持有期权合约数
 * // -- avgDelta: 策略平均每股Delta
 * // -- holdStockNum: 持有股票数
 * // -- holdStockCost: 持有股票成本价
 * // -- holdStockProfit: 持股盈亏
 * // -- totalStockCost: 股票总成本
 * // -- averageStockCost: 股票平均成本
 * // -- currentStockPrice: 当前股价
 * // -- putMarginOccupied: PUT订单保证金占用
 * // - orders: 订单数组，每条数据包含：
 * // -- id: 订单ID
 * // -- code: 证券代码
 * // -- market: 市场代码
 * // -- side: 订单方向（买入/卖出）
 * // -- price: 交易价格
 * // -- quantity: 交易数量
 * // -- orderFee: 交易费用
 * // -- tradeTime: 交易时间
 * // -- strikeTime: 行权时间
 * // -- status: 订单状态（已成交、已撤销、等待成交等）
 * // -- groupId: 订单组ID（当多笔订单具有相同的 `groupId` 时，表示它们属于同一笔交易操作，如Roll操作。）
 * // -- tradeFrom: 订单来源
 * // -- subOrder: 是否为子订单
 * // -- isOpen: 是否未平仓（期权订单特有，值为"未平仓"或"已平仓"）
 * // -- groupTotalIncome: 分组累计收益（分组订单特有）
 * // -- groupTotalOrderFee: 分组累计手续费（分组订单特有）
 * // -- ext: 扩展信息Map
 * // - orderGroups: 订单分组Map，key为groupId，value包含：
 * // -- totalIncome: 累计收益
 * // -- totalOrderFee: 累计手续费
 * // -- orderCount: 分组订单数
 *
 * @param strategyId 策略ID（strategyId）
 */
function queryStrategyDetailAndOrders(strategyId: string);

/**
 * 查询期权交易策略规则。策略详细内容包含具体的交易规则、delta要求、行权日期选择要求、技术指标要求等详细信息。
 * //returns 返回对象包含：
 * // - data: 策略规则数组，每条数据包含：
 * // -- code: 策略编码（如cc_strategy、wheel_strategy、default）
 * // -- title: 策略标题
 * // -- description: 策略描述
 * // -- content: 策略详细内容（支持Markdown格式）
 *
 * @param strategyCode? 期权策略编码，可选值：cc_strategy(备兑看涨策略)、wheel_strategy(车轮策略)、default(默认卖期权策略)，不指定时返回所有策略。
 */
function queryStrategyRule(strategyCode?: string);

/**
 * 查询指定股票的期权近10个到期日列表。
 * //returns 返回对象包含：
 * // - code: 股票代码
 * // - market: 市场代码
 * // - data: 到期日数组，每条数据包含：
 * // -- strikeTime: 到期日（YYYY-MM-DD格式）
 * // -- DTE: 距离到期日的天数
 * // -- tag: 期权标签（月期权/周期权）
 *
 * @param code 股票代码，如AAPL、TSLA等
 * @param market 市场代码：1(港股)|11(美股)
 */
function queryOptionsExpDate(code: string, market: number);

/**
 * 查询期权链详细信息。**使用前请先使用queryOptionsExpDate工具获取有效的到期日。**
 * //returns 返回对象包含：
 * // - code: 股票代码
 * // - market: 市场代码
 * // - strikeTime: 到期日
 * // - DTE: 距离到期日的天数
 * // - data: 期权数据数组，每条数据包含：
 * // -- code: 期权代码
 * // -- market: 市场代码
 * // -- delta: 希腊值Delta
 * // -- gamma: 希腊值Gamma
 * // -- theta: 希腊值Theta
 * // -- vega: 希腊值Vega
 * // -- rho: 希腊值Rho
 * // -- impliedVolatility: 隐含波动率（百分比数值，如20表示20%）
 * // -- premium: 溢价（百分比数值）
 * // -- curPrice: 当前价格
 * // -- openInterest: 未平仓数量
 * // -- volume: 成交量
 * // -- timeValue: 时间价值
 * // -- intrinsicValue: 内在价值
 * // -- sellAnnualYield: 卖出年化收益率（百分比数值，如24.33表示24.33%）
 * // -- strikePriceDistance: 行权价距离现价涨跌幅（百分比数值，如-3.5表示-3.5%）
 *
 * @param code 股票代码，如AAPL、TSLA等
 * @param market 市场代码：1(港股)|11(美股)
 * @param strikeDate 期权到期日，格式为YYYY-MM-DD，如2025-06-27。请先使用queryOptionsExpDate工具获取有效日期
 * @param filterType 期权类型过滤：PUT或CALL
 * @param tradeType 交易类型：SELL(卖出)或BUY(买入)。
 */
function queryOptionsChain(code: string, market: number, strikeDate: string, filterType: string, tradeType: string);

/**
 * 查询期权买卖盘报价数据。期权期权买卖盘信息，包括不同价位的买卖挂单数量和价格。
 * //returns 返回对象包含：
 * // - data: 买卖盘数据
 * // -- code: 期权代码
 * // -- market: 市场代码
 * // -- bidList: 买盘价格列表（按价格优先级排序）
 * // -- askList: 卖盘价格列表（按价格优先级排序）
 *
 * @param code 期权代码，如AAPL250620C150等
 * @param market 市场代码：1(港股)|11(美股)
 */
function queryOrderBook(code: string, market: number);

/**
 * 查询策略交易订单列表，策略ID必填，支持按订单状态、交易方向、标的代码、时间范围等条件筛选。
 * //returns 返回对象包含：
 * // - data: 订单数组，每条数据包含：
 * // -- id: 订单ID
 * // -- code: 证券代码
 * // -- market: 市场代码
 * // -- side: 订单方向（买入/卖出）
 * // -- price: 交易价格
 * // -- quantity: 交易数量
 * // -- orderFee: 交易费用
 * // -- tradeTime: 交易时间
 * // -- strikeTime: 行权时间
 * // -- status: 订单状态（已成交、已撤销、等待成交等）
 * // -- groupId: 订单组ID（相同groupId的订单属于同一笔组合交易，如Roll操作）
 * // -- tradeFrom: 订单来源
 * // -- subOrder: 是否为子订单
 * // -- isOpen: 是否未平仓（期权订单特有，值为"未平仓"或"已平仓"）
 * // -- groupTotalIncome: 分组累计收益（分组订单特有）
 * // -- groupTotalOrderFee: 分组累计手续费（分组订单特有）
 * // -- ext: 扩展信息Map
 * // - total: 总记录数
 * // - pageNum: 当前页码
 * // - pageSize: 每页大小
 * // - totalPages: 总页数
 *
 * @param strategyId 策略ID：订单所属交易策略的唯一标识（strategyId）
 * @param status? 订单状态：1-等待提交、2-提交中、5-已提交、10-部分成交、11-全部成交、14-部分成交已撤单、15-全部已撤单、21-下单失败、22-已失效、23-已删除、24-成交被撤销、25-提前指派
 * @param side? 交易方向：1-买入、2-卖出、3-卖空、4-买回
 * @param code? 标的代码：期权合约代码（如BABA260220C180000）或股票代码
 * @param orderId? 订单ID：订单唯一标识
 * @param startTime? 交易开始时间：格式yyyy-MM-dd HH:mm:ss
 * @param endTime? 交易结束时间：格式yyyy-MM-dd HH:mm:ss
 * @param pageNum? 页码：从1开始，默认1
 * @param pageSize? 每页大小：默认20，最大100
 */
function queryStrategyOrders(strategyId: string, status?: number, side?: number, code?: string, orderId?: string, startTime?: string, endTime?: string, pageNum?: number, pageSize?: number);

```
