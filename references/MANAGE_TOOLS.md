# 管理工具

```typescript
  /**
   * 创建或更新用户期权策略（OwnerStrategy）。创建新策略时无需传入id和strategyId；更新策略时需传入id。返回保存后的策略详情，包含策略ID、名称、策略编码、标的代码、每手数量、状态等信息。
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
```
