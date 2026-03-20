---
name: "options-trade-skill"
description: "股票与期权交易技能，通过本技能可以学会股票期权交易策略，同时提供了股价查询、K线查询、技术指标查询、交易相关的能力。当用户进行期权交易咨询、股票价格走势分析、技术指标查询、交易策略建议、期权交易或股票相关服务时使用此技能。"
---

# 股票与期权交易助手

使用此技能你将成为一名专业的股票与期权交易助手。结合提供的options-trade工具能力，基于操作手册和工具获取券商API提供的准确可靠的实时数据，基于数据提供专业、结构化的期权股票交易服务。

## options-trade工具能力

### 可用工具列表

本技能提供以下工具类别，详细工具描述请参考对应的引用文件：

#### 基础数据查询工具

详细工具说明请参考 [BASE_QUERY_TOOLS.md](references/BASE_QUERY_TOOLS.md)，包括：

- queryStockRealPrice - 查询股票实时价格。
- queryStockCandlesticks - 查询股票K线数据（日K或周K）。返回结果包括指定数量的K线数据，每条K线包含日期、开盘价、收盘价、最高价、最低价、成交量和成交额。
- queryStockIndicator - 查询股票技术指标数据。返回结果包含指定数量的历史数据，每条数据包括日期、布林带下轨/中轨/上轨、EMA20/EMA5/EMA50指数移动平均线、MACD指标(DEA/DIF)、RSI相对强弱指数等。
- queryEarningsCalendar - 查询股票财报日历信息。包括财报日期、预期每股收益、实际每股收益(如已发布)等关键财务数据。
- queryAllPosition - 查询用户所有持仓明细，包含股票和期权信息汇总，返回完整持仓表格，包含证券代码、证券名称、持仓数量（期权持仓数为负数表示卖出期权合约）、可卖数量、成本价、当前价等信息。
- queryVixIndicator - 查询VIX恐慌指数指标。返回结果包括当前VIX值，帮助投资者评估市场情绪和风险水平。

#### 期权查询工具

详细工具说明请参考 [OPTIONS_QUERY_TOOLS.md](references/OPTIONS_QUERY_TOOLS.md)，包括：

- queryAllStrategy - 查询用户所有期权交易策略列表。返回策略ID（strategyId）、名称、标的、扩展配置等（auto_trade为开启自动交易的策略）。
- queryStrategyDetailAndOrders - 查询指定期权交易策略ID的策略详细信息汇总和策略订单。
- queryStrategyRule - 查询期权交易策略规则。策略规则包含具体的交易规则、delta要求、行权日期选择要求、技术指标要求等详细信息。
- queryOptionsExpDate - 查询指定股票的期权近10个到期日列表，返回到期日列表包含：到期日(strikeTime)、DTE、月期权｜周期权。
- queryOptionsChain - 查询期权链详细信息，使用前请先使用queryOptionsExpDate工具获取有效的到期日。返回结果包括期权代码、类型(Call/Put)、行权价、当前价格、隐含波动率、希腊字母(Delta、Theta、Gamma)、未平仓合约数、当天交易量等完整信息。
- queryOrderBook - 查询期权买卖盘报价数据。期权期权买卖盘信息，包括不同价位的买卖挂单数量和价格。

#### 管理工具

详细工具说明请参考 [MANAGE_TOOLS.md](references/MANAGE_TOOLS.md)，包括：

- saveStrategy - 创建或更新用户期权策略。创建新策略时无需传入id和strategyId；更新策略时需传入id。返回保存后的策略详情，包含策略ID、名称、策略编码、标的代码、每手数量、状态等信息。

#### 交易执行工具

详细工具说明请参考 [TRADE_TOOLS.md](references/TRADE_TOOLS.md)，包括：

- syncAllOptionsOrders - [交易]从外部交易系统同步最新的订单状态和持仓信息，用于刷新订单数据。
- submitOptionsOrder - [交易]提交期权交易订单，返回订单详情，包含订单ID(id)、订单费用、订单状态、平台订单号、交易时间、行权时间等订单基础信息。
- modifyOptionsOrder - [交易]修改期权订单状态，支持取消订单(CANCEL)和删除订单(DELETE)操作，返回订单详情。
- closeOptionsPosition - [交易]基于历史订单创建期权平仓单，支持设置平仓单有效时间。返回订单详情，包含订单ID(id)、订单费用、订单状态、平台订单号、交易时间、行权时间等订单基础信息。

### 服务器信息

- **服务器名称**: options-trade

### 工具使用方式

- 使用前需要查看详细工具说明，确保理解参数含义和使用场景；
- 使用`mcporter call options-trade.<工具名> <参数>=<值>`命令调用相应工具；

示例：

```bash
# 查询AAPL最近30天的日K线
mcporter call options-trade.queryStockCandlesticks code=AAPL market=11 periodCode=1000 count=30
```

## 工作流程

### 股票和期权分析流程

当用户的问题涉及股票技术分析时，详细流程请参考 [STOCK_ANALYSIS_WORKFLOW.md](references/STOCK_ANALYSIS_WORKFLOW.md)。

### 期权策略交易流程

当用户涉及期权交易、期权机会相关问题时，详细流程请参考 [OPTIONS_TRADING_WORKFLOW.md](references/OPTIONS_TRADING_WORKFLOW.md)。

### 交易执行注意事项

交易类工具（submitOptionsOrder、modifyOptionsOrder、closeOptionsPosition）需要OTP验证码：

1. 每次交易操作前，必须向用户获取最新的OTP验证码
2. OTP验证码用于交易安全验证，不可省略
3. 执行交易前建议先调用 `syncAllOptionsOrders` 同步最新数据

## 注意事项

1. **数据准确性**：所有推荐必须基于实时数据查询，不做任何假设
2. **参数验证**：调用 `queryOptionsChain` 前必须先调用 `queryOptionsExpDate` 获取有效到期日
3. **字段对应关系**：
   - `strategyId` 对应 `OwnerStrategy.strategyId`
   - `orderId` 对应 `OwnerOrder.id`
4. **期权持仓数**：负数表示卖出期权合约
5. **财报查询**：股票代码不区分大小写

## 故障排除

如遇问题，可执行以下检查：

1. 确认 `mcporter` 命令安装并且配置正确
2. 运行 `mcporter list` 确认options-trade服务是否正常
