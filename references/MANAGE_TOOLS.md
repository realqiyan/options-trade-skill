# 管理工具

```typescript
/**
 * 创建或更新用户期权策略。创建新策略时无需传入id和strategyId，更新策略时需传入id。返回保存后的策略详情。
 * //returns 返回对象包含：
 * // - data: 保存后的策略信息
 * // -- id: 策略主键ID
 * // -- strategyId: 策略唯一标识符
 * // -- strategyName: 策略名称
 * // -- strategyCode: 策略编码
 * // -- stage: 策略阶段
 * // -- startTime: 策略开始时间
 * // -- code: 标的代码
 * // -- lotSize: 每手数量
 * // -- stage: 策略阶段
 * // -- status: 策略状态
 * // -- ext: 扩展配置
 * // - success: 是否成功
 * // - message: 操作结果消息
 *
 * @param id? 策略ID（更新时必填，创建时不填）
 * @param strategyName 策略名称，如：BABA车轮策略
 * @param strategyCode 策略编码：wheel_strategy（车轮策略）、cc_strategy（备兑看涨策略）、default（默认卖期权策略）
 * @param code 标的代码，如：BABA、AAPL
 * @param lotSize 每手数量，美股期权默认为100
 * @param stage 策略阶段：running（运行中）、suspend（暂停）
 * @param status? 策略状态（1=启用，0=禁用），默认1
 * @param extJson? 扩展配置JSON字符串，如：{"auto_trade":"true","target_delta":"0.3"}
 */
function saveStrategy(id?: number, strategyName: string, strategyCode: string, code: string, lotSize: number, stage: string, status?: number, extJson?: string);

/**
 * [策略]将一个策略绑定多个订单，支持部分成功返回明细。
 *
 * //returns 返回对象包含：
 * // - data: 绑定结果
 * // -- owner: 用户编码
 * // -- strategyId: 策略ID
 * // -- strategyCode: 策略标的代码
 * // -- totalCount: 总订单数
 * // -- successCount: 成功数量
 * // -- failureCount: 失败数量
 * // -- partialSuccess: 是否部分成功
 * // -- message: 汇总消息
 * // -- successList: 成功明细
 * // -- failureList: 失败明细（含errorCode/message）
 *
 * @param strategyId 策略ID（strategyId）
 * @param orderIds 订单ID列表（如[1,2,3]）
 */
function bindStrategyOrders(strategyId: string, orderIds: number[]);
```
