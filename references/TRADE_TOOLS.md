# 交易工具

```typescript

  /**
   * [交易]从外部交易系统同步最新的订单状态和持仓信息，用于刷新订单数据。
   */
  function syncAllOptionsOrders();

  /**
   * [交易]提交期权交易订单，返回订单详情（OwnerOrder），包含订单ID(id)、订单费用、订单状态、平台订单号、交易时间、行权时间等订单基础信息。
   *
   * @param strategyId 策略ID：订单所属策略的唯一标识（OwnerStrategy.strategyId）
   * @param side 交易方向：1-买入、2-卖出
   * @param quantity 期权合约的张数
   * @param price 期权合约的每股价格（元）
   * @param code 期权标的码：BABA260220C180000
   * @param market 市场代码：1表示港股，11表示美股
   * @param otp OTP验证码：用于交易安全验证，每次操作需要向用户获取最新的OTP验证码
   */
  function submitOptionsOrder(strategyId: string, side: number, quantity: number, price: number, code: string, market: number, otp: string);

  /**
   * [交易]修改期权订单状态，支持取消订单(CANCEL)和删除订单(DELETE)操作，返回订单详情。
   *
   * @param orderId 订单ID：需要操作的期权订单唯一标识（OwnerOrder.id）
   * @param action 操作类型：CANCEL-取消未成交的订单，DELETE-删除已取消或已完成的订单
   * @param otp OTP验证码：用于交易安全验证，每次操作需要向用户获取最新的OTP验证码
   */
  function modifyOptionsOrder(orderId: string, action: "CANCEL" | "DELETE" | "UNKNOWN", otp: string);

  /**
   * [交易]基于历史订单创建期权平仓单，支持设置平仓单有效时间。返回订单详情（OwnerOrder），包含订单ID(id)、订单费用、订单状态、平台订单号、交易时间、行权时间等订单基础信息。
   *
   * @param orderId 订单ID：需要平仓的期权订单唯一标识（OwnerOrder.id）
   * @param price 平仓价格：期权合约的每股价格（美元）
   * @param cannelTime 平仓截止时间：订单将在此时间前尝试平仓，格式：yyyy-MM-dd HH:mm:ss
   * @param otp OTP验证码：用于交易安全验证，每次操作需要向用户获取最新的OTP验证码
   */
  function closeOptionsPosition(orderId: string, price: number, cannelTime: string, otp: string);

```
