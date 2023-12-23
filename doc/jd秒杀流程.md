# jd秒杀流程



##  秒杀流程

1. api.m.jd.com/client.action?functionId=genToken 生成 tokenkey 和转跳地址
2. 经过 2~3 次转跳获取 seckill.action，如果遇到marathon.jd.com/mobile/koFail.html 则重新 genToken。
3. 访问 marathon.jd.com/seckillM/seckill.action
4. 调用marathon.jd.com/seckillnew/orderService/init.action 获取地址发票相关信息
5. 调用gia.jd.com/jsTk.do 获取 eid 和 token
6. gen_order_data,组织数据，生成订单信息
7. marathon.jd.com/seckillnew/orderService/submitOrder.action

---

*经测试，抢mate60的时候前几步都可以在抢购之前执行，到点执行6，7就行。所以mate抢到的概率很大。*

*茅台则必须到点按流程执行。*

