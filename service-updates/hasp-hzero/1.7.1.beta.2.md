# 1.7.1.BETA.2

_**`hssp-service`**_** ** ![](https://img.shields.io/badge/-1.7.1.BETA.2-brightgreen)

{% code overflow="wrap" lineNumbers="true" %}
```log
- e74c3db18c [FIX]hfins-3136:【我的应付】关联合同金额校验问题

- 3003a13d26 [FIX][hfins-3069]费用明细查询多选框，主键加密bug

- 884714f50e [FIX-hfins-3110]：【总账报账单类型定义】付款/冻结类的单据分配附件类型时，系统报错

- 9ed5a65964 [FIX]bugfix-hfins-3113:费用分摊查询未加密报错

- aea55b6c87 [FIX]hfins-3091:【我的预提申请】生成反冲的预提申请单时，需清空最后审核人和最后审核时间

- 662ce12731 [FIX]hfins-3089:【我的预提申请】预提单走共享流程，复核未变更总账接口标志

- 4842787ad7 [FIX]hfins-3012:【APP】还款单详情，点击查看关联借款单单据编号报错

- 08b8266ea2 [FIX]bugfix-hfins-2820报销单复制时添加智能检查状态记录

- 7872ae8299 [FIX][hfins-2985]报销单分摊对象主键加密bug

- 66328ef1c6 [FIX]bugfix-hfins-2989 :【费用摊销计划】筛选条件来源单据没有作用

- d23ffc16fb [FIX]bugfix-hfins-3000 :【预提申请单类型定义】点击多语言报错

- dd0d5f06d0 [FIX]bugfix-hfins-3002 :【摊销计划类型定义】点击多语言框报错

- a002764903 [FIX]bugfix-hfins-2995:【筛选规则定义】多语言查询有问题

- 225259b9ce [FIX-hfins-3004]：【我的应付报账单】调整类的应付报账单，点击关联蓝字发票时报错

- f486ab21 [FIX-hfins-2925] 解决海马汇服务合并后 Feign value 指定原服务名导致调用不通的问题

...
```
{% endcode %}



_<mark style="color:green;">更新说明</mark>_

1、配置

海马汇 `Feign` 调用时 `Value` 提供环境变量设置，可配置如下：

{% code overflow="wrap" lineNumbers="true" %}
```yaml
hippius:
  service:
    platform: 
      name: ${HIPPIUS_SERVICE_PLATFORM_NAME:hippius-all}
    submenu:
      name: ${HIPPIUS_SERVICE_SUBMENU_NAME:hippius-all}
    pushcenter:
      name: ${HIPPIUS_SERVICE_PUSHCENTER_NAME:hippius-all}
```
{% endcode %}



