<p align="center">
  <a href="https://github.com/popjane/v-api"><img src="./images/logo.svg" width="125" height="125" alt="v-api"></a>
</p>

<div align="center">

# V-API

✨ 功能强大的ai模型网关管理平台，开箱即用 ✨

</div>

> [!NOTE]
> 本项目为闭源项目，仅支持授权使用！
> 前端UI基于[semi.design](https://semi.design/zh-CN/start/introduction)，后端基于[one-api](https://github.com/songquanpeng/one-api)、部分功能来自[new-api](https://github.com/Calcium-Ion/new-api)
>
> 👉 [项目演示](https://api.v3.cm/)

> [!IMPORTANT]
> 根据[《生成式人工智能服务管理暂行办法》](http://www.cac.gov.cn/2023-07/13/c_1690898327029107.htm)的要求，请勿对中国地区公众提供一切未经备案的生成式人工智能服务。
> 该项目API仅用于非商业性的学习、研究、科研测试等合法用途，不得用于任何违法违规用途以及商业用途，否则后果自负。

> [!TIP]
> 郑重声明：本项目前端UI为原创设计，同类中转项目如有雷同，皆为盗版抄袭！

## 项目介绍

一、基础功能：支持one-api所有功能，支持new-api的midjourney、suno、realtime、易支付功能。

二、特色功能：

1. 公告系统（type = 1 系统公告 | 2 调价公告）：完全独立的公告系统，支持公告邮件推送、TG频道自动推送。
2. 推广返利系统：支持推广返利，支持自定义返利比例、返利次数、支持奖励提现、独立的奖励日志、反作弊。
3. 开票系统：支持用户在线申请开票，在线审核，在线发送邮件。
4. 任务系统：支持可灵、runway、luma、ideogram、mj、visual等众多图片音频视频任务，并且不断更新支持更多平台。
5. 上游管理系统：工厂封装上游平台，支持一站式管理上游令牌（增删改查）、统计渠道成本、快速核对上游消耗成本。
6. 邮件群发系统：可针对不同月份未登录用户进行群发邮件。
7. 原子无锁设计：移除原系统大量高频的锁设计，改为支持高并发的保证原子性的无锁设计。
8. 充值首单优惠：支持首单优惠，支持自定义优惠金额。
9. 限时活动系统：支持开启充值限时活动，倒计时结束自动恢复充值价格。
10. 模型体验功能：用户可在模型价格页直接体验模型聊天，无需绑定key。
11. 渠道管理功能：针对渠道管理做了大量优化，支持渠道克隆、渠道余额预警、批量启用禁用、批量删除、一键替换等。
12. 模型联网功能：支持任意chat模型联网搜索功能。
13. 模型详情系统：支持增删改模型详情介绍，支持模型详情页展示、支持在线体验模型。
14. 订阅通知系统：用户可订阅站内事件，触发时自动发送邮箱通知。
15. 订单管理系统：独立的订单管理，快速查询用户充值情况。
16. SEO优化：支持自定义SEO关键词、描述、标题 皆为ssr渲染。
17. 帮助中心优化：支持自定义帮助中心新手教程、应用教程。
18. 首页主题切换：已内置首页多主题设计，按需加载，后续将新增更多的首页模板。
19. 更多自定义功能：自定义页脚、悬浮客服、侧边栏广告……

三、拓展功能：

1. 注册登录增强：支持记录注册时间、注册ip、最后登录ip、支持google登录、支持oidc登录。
2. 找回密码增强：找回密码发送至邮箱，安全性更高。
3. 更强大的仪表盘图表：支持7天数据看板、当日数据看板。
4. 更强大的令牌分组管理、倍率管理。
5. 可限制用户可创建令牌数量。
6. 支持perplexity。
7. 支持claude原生请求格式。
8. 隐藏上游敏感错误：包括分组信息，大量敏感的错误信息，保护平台隐私。
9. 优化日志清理阻塞问题。
10. Redis缓存大量优化：墙裂建议开启redis使用，可以大大提高并发与请求速度。
11. 充值网关支持自定义。
12. 支持仅测试自动禁用的渠道（该模式-永不自动测试已手动禁用的渠道、已启用的渠道为被动自动测试）
13. 多语言支持。

更多大量的细节优化，欢迎体验！

## 环境变量设置

支持[one-api](https://github.com/songquanpeng/one-api?tab=readme-ov-file#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F) 所有环境变量，额外新增如下环境变量：

| 变量名 | 默认值 | 说明 |
| --- | --- | --- |
|MY_MEMORY_ENABLED|false|内存缓存，只同步主从节点的`Option`配置：由于`MEMORY_CACHE_ENABLED`会造成渠道的启用禁用以及增删模型都不是实时的，因此可单独配置该参数。与`MEMORY_CACHE_ENABLED`二选一。高并发用户不建议开启。|
|MY_REDIS|false|该模式（不缓存用户额度）。与`REDIS_CONN_STRING`二选一。唯一区别是预扣费时是从数据库读取用户余额而并非Redis。高并发用户不建议开启。|
|VAPI_KEY|-|（必须）系统授权令牌：用于验证VAPI系统授权|
|VAPI_SECRET|-|（必须）系统授权秘钥：用于验证VAPI系统授权|
|S3_BUCKET|-|S3存储桶名称，站内上传图片、文件配置，任意的支持aws-s3的存储都支持|
|S3_KEY_ID|-|S3存储桶key，站内上传图片、文件配置，任意的支持aws-s3的存储都支持|
|S3_KEY_SECRET|-|S3存储桶secret，站内上传图片、文件配置，任意的支持aws-s3的存储都支持|
|S3_ENDPOINT|-|S3存储桶endpoint，站内上传图片、文件配置，任意的支持aws-s3的存储都支持|
|UPDATE_TASK|true|是否更新Task异步任务，若无任务模型，可关闭该配置，仅需在主节点配置即可|

## 相关截图

待更新...
