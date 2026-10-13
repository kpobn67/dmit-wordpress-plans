# DMIT WordPress：$10.9/月起挑对套餐，把博客、企业站和外贸站跑稳的选机与配置思路

搜 “DMIT WordPress” 的人，多半卡在同一个地方：知道自己要拿 DMIT 跑 WordPress，但一进官网就懵了——洛杉矶、香港、东京三个机房，每个机房里又分 Premium、Eyeball、Tier 1 三条线路，再叠上 AS3、AN4、AN5 三种硬件平台，套餐名字全是 `LAX.AS3.Pro.TINY` 这种缩写，价格从一年 36.9 美元跳到一个月 199.9 美元。

更关键的一点得先说清楚：**DMIT 卖的是 KVM 虚拟服务器（VPS），不是 WordPress 托管主机。** 它不会帮你装 WordPress、不会帮你迁站、不会帮你做网站备份。你拿到的是干净的 Linux 系统和 root 权限，Nginx、PHP、数据库、SSL 这些都得自己搭。想清楚这件事，后面的选套餐才有意义——你要挑的不是“WordPress 套餐”，而是“一台配置够用、线路适合你的服务器的机器”。

## 先算清楚：一个 WordPress 站到底吃多少资源

网上讨论 DMIT 的文章大多在聊线路和延迟，很少有人先回头算一笔账。其实 WordPress 的资源需求相当固定：

- **内存**：1GB 能跑起来，但装上 WooCommerce、缓存插件和 Redis 之后会开始吃紧。2GB 是更舒服的起步线，同时跑两个站建议 4GB。
- **硬盘**：系统加 LNMP 环境大约占掉 3–5GB，WordPress 本体加插件主题不到 1GB。20GB SSD 放过两三个轻量站没问题，但只要站内图片多、或者打算存备份文件，80GB 起步更省心。
- **CPU**：普通内容站 1 核够用，缓存配好之后并发压力主要落在 PHP 上，2 核会让后台操作和插件更新流畅不少。
- **流量**：个人博客和中小型企业站每月几十 GB 很常见。但这里有个 DMIT 的特性要特别注意——**它按双向计费**，进出的较大者算一次，大图站和下载站的实际消耗会比按单向计费的家商高一截。

按这个标准去看 DMIT 的产品线，你会发现大部分中高端套餐对 WordPress 来说是性能过剩的，真正值得纠结的是线路和预算。

## 三条线路、三个机房，对应的是三类完全不同的 WordPress 站

DMIT 的产品逻辑不是按 CPU 分档，而是按“网络路由”分档。同一个机房同样配置，价格能差一倍，差的就是这个。

| 线路系列 | 网络特点 | 中国电信访问 | 适合的 WordPress 场景 |
| --- | --- | --- | --- |
| Premium（Pro） | 含 Tier 1 Transit + 中国电信 CN2 GIA 等高级资源 | 三网回程走 CN2 GIA，晚高峰相对稳 | 中文博客、企业官网、面向国内用户的正式站点 |
| Eyeball（EB） | Tier 1 基础上尽力优化中国方向，走 CMIN2 / 9929 | 电信走 9929/58807 负载，联通走 9929，移动走 CMIN2 | 移动、联通用户为主的站，同价位流量给得更多 |
| Tier 1（T1） | 纯国际优化路由，不含中国大陆专项优化 | 无优化，可能绕路 | 面向海外读者的英文站、外贸站、测试环境、备份节点 |

机房的选择逻辑比线路更简单：

- **洛杉矶（LAX）**：单价最低、套餐最全、补货最勤。面向北美和全球用户首选，也是预算有限时的默认答案。
- **香港（HKG）**：到内地物理距离近，适合主要读者在国内、又不想备案的站。代价是同配置价格明显更高。
- **东京（TYO）**：面向日本和东亚用户，Pro 系列走三网 CN2 GIA。库存一直比较紧俏。

一个容易被忽略的细节：DMIT 支持**跨机房内网互通**，香港—美国、日本—美国、香港—日本之间可以走内网传数据。如果你的 WordPress 用一台机器跑站、另一台在别的机房做异地备份，这件事能省掉一部分公网流量。

## DMIT 洛杉矶 AS3 全套餐价格表

AS3 是 AMD EPYC 7003 平台，属于目前在售平台里门槛最低的一档，也是补货最稳定的一档。下面这三个系列覆盖了绝大多数 WordPress 用户的实际需求。

### Premium（CN2 GIA）——国内读者的站优先看这组

| 套餐 | CPU | 内存 | SSD | 月流量 / 带宽 | 超量后 | 价格（月付） | 购买 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| LAX.AS3.Pro.TINY | 1 核 | 2GB | 20GB | 1TB / 1Gbps | 4Mbps 不限流 | $10.90 | [ 看 TINY 当前库存与价格](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.Pocket | 2 核 | 2GB | 40GB | 1.5TB / 4Gbps | 4Mbps 不限流 | $16.90 | [ 用 Pocket 起步建站](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.STARTER | 2 核 | 2GB | 80GB | 3TB / 10Gbps | 4Mbps 不限流 | $34.90 | [ 查看 STARTER 配置详情](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MINI | 4 核 | 4GB | 80GB | 5TB / 10Gbps | 8Mbps 不限流 | $62.90 | [ 选 MINI 跑多站](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MICRO | 4 核 | 4GB | 160GB | 7TB / 10Gbps | 8Mbps 不限流 | $87.90 | [ 查看 MICRO 套餐](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MEDIUM | 6 核 | 8GB | 160GB | 14TB / 10Gbps | 10Mbps 不限流 | $199.90 | [ 了解 MEDIUM 高配方案](https://www.dmit.io/aff.php?aff=12046) |

线路走向：电信去程走 CN2 GIA（AS4809），联通去程直连 AS4837，移动去程经香港移动（AS58453），三网回程统一走 AS4809。

### Eyeball（CMIN2 / 9929）——同价位流量多一半

| 套餐 | CPU | 内存 | SSD | 月流量 / 带宽 | 超量后 | 价格（月付） | 购买 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| LAX.AS3.EB.TINY | 1 核 | 2GB | 20GB | 1.5TB / 2Gbps | 4Mbps 不限流 | $10.90 | [ 查看 EB TINY 套餐](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.Pocket | 2 核 | 2GB | 40GB | 3TB / 4Gbps | 4Mbps 不限流 | $16.90 | [ 用 EB Pocket 建站](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.STARTER | 2 核 | 2GB | 80GB | 5TB / 10Gbps | 4Mbps 不限流 | $34.90 | [ 看 EB STARTER 当前价格](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MINI | 4 核 | 4GB | 80GB | 10TB / 10Gbps | 8Mbps 不限流 | $62.90 | [ 选择 EB MINI](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MICRO | 4 核 | 4GB | 160GB | 14TB / 10Gbps | 8Mbps 不限流 | $87.90 | [ 查看 EB MICRO 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MEDIUM | 6 核 | 8GB | 160GB | 30TB / 10Gbps | 10Mbps 不限流 | $199.90 | [ 了解 EB MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

同样是 10.9 美元一个月，EB 的 TINY 给你 1.5TB 流量和 2Gbps 端口，Pro 只给 1TB 和 1Gbps。如果你的读者以移动或联通为主，EB 这组更划算；如果电信用户占比高、又跑的是正式业务，Pro 的 CN2 GIA 回程更省心。这条判断在多个主机社区的实测讨论里都能对上。

### Tier 1（国际线路）——门槛最低的一组

| 套餐 | CPU | 内存 | SSD | 月流量 / 带宽 | 超量后 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| LAX.AS3.T1.WEE | 1 核 | 1GB | 20GB | 1TB / 4Gbps | 100Mbps 不限流 | $36.90 / 年 | [ 用 WEE 年付开机](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.T1.TINY | 1 核 | 1GB | 20GB | 2TB / 4Gbps | 200Mbps 不限流 | $6.90 / 月 | [ 查看 T1 TINY 套餐](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.T1.STARTER | 1 核 | 2GB | 40GB | 4TB / 10Gbps | 200Mbps 不限流 | $12.90 / 月 | [ 选 T1 STARTER 建站](https://www.dmit.io/aff.php?aff=12046) |

> WEE 的年付价格折算下来每月三美元出头，是 DMIT 全线里门槛最低的一档。代价是没有中国大陆线路优化，电信用户访问体验会比较随机。

价格和库存这两个数字在 DMIT 身上都不太稳，促销、补货、售罄轮着来。上面所有价格下单前都值得在结算页再核一遍。

## 香港和东京：什么时候值得多花这笔钱

如果你的站主要面向国内读者，香港的地理优势是实打实的。代价也不小：

**香港 Premium AS3（三网 CN2 GIA）**

| 套餐 | CPU | 内存 | SSD | 月流量 | 价格（月付） | 购买 |
| --- | --- | --- | --- | --- | --- | --- |
| HKG.Pro.TINY | 1 核 | 1GB | 20GB | 500GB | $39.90 | [ 查看香港 Pro TINY](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.STARTER | 1 核 | 2GB | 40GB | 1TB | $79.90 | [ 看香港 Pro STARTER](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.MINI | 2 核 | 2GB | 60GB | 1.5TB | $126.90 | [ 选择香港 Pro MINI](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.MICRO | 4 核 | 4GB | 80GB | 2TB | $179.90 | [ 查看香港 Pro MICRO](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.MEDIUM | 4 核 | 8GB | 160GB | 2.5TB | $239.90 | [ 了解香港 Pro MEDIUM](https://www.dmit.io/aff.php?aff=12046) |

香港 T1 系列便宜得多，WEE 年付 $36.90、TINY $6.90/月、STARTER $12.90/月，但它是国际 BGP 线路，对内地没有优化。用香港 T1 跑面向国内读者的 WordPress，可能出现“花钱买了香港 IP，速度还不如洛杉矶 Pro”的结果，这是选香港时最容易踩的坑。

东京这边，TYO.Pro.TINY 是 $21.90/月（1 核 / 1GB / 20GB / 500GB 流量，1Gbps），TYO T1 TINY 则是 $6.90/月。日本 Pro 的库存长期偏紧，看到有货别拖太久。

## 新平台 AN4 / AN5 值不值得多掏钱

DMIT 洛杉矶在 AS3 之外还有 AN4（EPYC 9004）和 AN5（EPYC 9005）两个更新的平台。同名字套餐，平台不同价格也不同，比如 LAX.Pro 系列在不同平台上的报价大致是 AS3 最低、AN4 居中、AN5 最高。

对 WordPress 来说，这个差价大概率不值。CMS 的性能瓶颈在 PHP 执行和数据库查询上，9005 比 7003 多出来的单核性能，在装好对象缓存、页面缓存的站上几乎感受不到。AS3 反而因为成熟稳定、价格低、库存相对充足，更适合作为长期跑站的平台。真要为新平台加价，理由应该是你要在同一台机器上跑更重的业务，而不是“跑 WordPress 会更快”。

这里有个报价上的分歧需要提醒：AN5 平台的入门款在不同渠道出现过 $12.98/月 和 $14.9/月 两种说法，可能是补货批次或套餐版本不同。别照着文章里的数字下单，进结算页看实际价格。

## 从开机到 WordPress 跑起来，实际要走这几步

DMIT 提供的是纯 KVM 机器，默认走 SSH 密钥登录。整个流程大致是：

1. 下单后拿到 IP 和 root 权限，用密钥登录系统，先改端口、配防火墙。
2. 装环境。想省事就用宝塔面板或 aaPanel，想干净就上 LNMP 一键包。PHP 建议 8.0 以上，数据库用 MariaDB 或 MySQL 8。
3. 建站、绑域名。域名解析到服务器 IP，DMIT 不提供域名注册和 DNS 托管，这部分要自己在别处做。
4. 装 SSL。Let's Encrypt 免费证书足够，配好之后记得设置自动续期。
5. 加缓存。对象缓存（Redis）加页面缓存，1 核 2GB 的机器跑一个中等流量的内容站会轻松很多。
6. 做备份。这一条要格外强调：**DMIT 不负责你网站文件的备份，机器丢了、误删了，恢复不了。** 站内备份要通过插件同步到对象存储或另一台服务器。

如果你完全不想碰命令行、也不想管服务器维护，那 DMIT 这套方案本身就不适合你——它省的是钱，花的是你的时间。

## 优惠码和退款：下单前值得花两分钟确认的事

DMIT 的促销节奏和不少商家不一样，很少有全场大促，优惠码数量少、更新慢，且大多限定具体产品线和付款周期。目前第三方整理出来、被多个来源提到过的几个是：

- `LAX-EB-LAUNCH-NON-MONTHLY-RECURRING-20OFF`：洛杉矶 EB 系列 Tiny 及以上，非月付，8 折循环优惠
- `202510_HKG_TYO_PRO_20OFF_RECURRING`：香港 / 东京 Pro 系列，季付及以上，8 折循环
- `202510_HKG_TYO_T1_30OFF_RECURRING`：香港 / 东京 T1 系列，季付及以上（不含 WEE），7 折循环
- `Lite-Annually-Recur-30OFF` / `Lite-Semi-Annually-Recur-20OFF`：标准网络系列年付 7 折、半年付 8 折

所谓“循环”，意思是续费也按折扣价走，不是只便宜第一单。但这些码来自第三方整理，有效性随时可能变化，结算时点一下 Validate Code 验证一下，能用就用，用不了也别意外。

退款方面，DMIT 的政策是 3 天内且流量不超过 30GB 可全额退款，之后 30 天内按剩余价值比例退，续费订单和余额支付不适用。条款细节建议在下单前跟客服或结算页再确认一次。付款方式覆盖支付宝、微信、PayPal 和信用卡，有中文客服。

## 几个常见问题

**DMIT 的机器需要备案吗？**
不需要。洛杉矶、香港、东京都是海外机房。

**流量用完了会停机吗？**
不会。超出套餐额度后自动降速继续跑，Pro / EB 的入门款降到 4Mbps，T1 系列降到 100–200Mbps。这是 DMIT 比较友好的一点设计，至少不会某天早上醒来网站打不开。

**IP 被墙了怎么办？**
DMIT 支持换 IP，条件符合时可以免费更换，其余情况按次收费，具体规则和频率在官网帮助文档里有说明，下单前可以先看一眼。

**能解锁流媒体吗？**
DMIT 标配原生 IP，社区实测里能解锁 Netflix、TikTok、ChatGPT 等服务的案例不少，但商家不做保证，也没有 SLA 承诺，需要自己测试。

**一年 36.9 美元那台能跑 WordPress 吗？**
技术上能。T1.WEE 是 1 核 1GB，装个轻量 LNMP、关掉重型插件、配好缓存，跑一个纯文字博客是可以的。但只要你想上 WooCommerce、图片多、或者读者主要在国内，这台机器很快就会让你难受。省下来的钱最后会被你花在迁移和折腾上。

## 落到具体建议

大致可以这样分：

- **中文博客 / 企业官网 / 外贸站，读者在国内** → LAX.AS3.Pro.TINY（$10.90/月）起步，流量或并发上来后升 Pocket、STARTER。
- **读者以移动、联通为主，想多要流量** → LAX.AS3.EB.TINY，同样 $10.90/月，1.5TB 流量。
- **英文站、面向北美或全球读者，预算敏感** → LAX.AS3.T1.WEE，年付 $36.90。
- **主要读者在国内，对访问速度要求高且预算充足** → 香港 Pro 系列，但别为了“香港 IP”这个名头去选香港 T1。

VPS 这类产品最好的习惯是先用月付试一个月，把自己的站实际跑上去看后台响应和读者反馈，满意了再转年付。DMIT 的库存和价格都变得快，看到合适的机器有货，比等到最低价更重要。

想直接看当前在售套餐和库存状态，可以从这里进：[👉 查看 DMIT 全部套餐与实时价格](https://www.dmit.io/aff.php?aff=12046)。
