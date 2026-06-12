# Shadowrocket Config

Shadowrocket 订阅配置：

```text
https://raw.githubusercontent.com/xinworks/ssconfig/main/sr.conf
```

## 策略总览

```text
流量进入
  |
  +-- 私网/本地地址
  |      -> 绕过代理
  |
  +-- 加密相关域名
  |      -> 🪙 加密策略
  |           默认: 🇯🇵 日本出口
  |           可选: 美国 / 新加坡 / DIRECT
  |
  +-- 金融相关域名
  |      -> 🏦 金融策略
  |           默认: 🇸🇬 新加坡节点
  |           当前包括: OCBC / IBKR / 老虎证券 / 富途 / 长桥
  |
  +-- 国内服务规则
  |      -> 🏠 国内服务
  |           默认: DIRECT
  |           可选: 新加坡 / 美国 / 日本
  |
  +-- 国际服务规则集
  |      -> 🌍 国际服务
  |           默认: 🇺🇸 美国节点
  |           可选: 日本 / 新加坡 / DIRECT
  |
  +-- 其它所有未命中
         -> 🌐 默认出口
              默认: 🇺🇸 美国节点
              可选: 日本 / 新加坡 / DIRECT
```

## 匹配顺序

规则按顺序匹配，先命中先使用：

```text
1. 加密相关服务 -> 🪙 加密策略
2. OCBC / IBKR / 老虎证券 / 富途 / 长桥 -> 🏦 金融策略
3. 国内服务 / CN / Apple / Microsoft -> 🏠 国内服务
4. 国际代理规则 -> 🌍 国际服务
5. 其它所有 -> 🌐 默认出口
```

## 策略组

```text
🪙 加密策略
  默认: 🇯🇵 日本出口
  用途: Bybit 等加密相关服务，默认走日本出口

🏦 金融策略
  默认: 🇸🇬 新加坡节点
  用途: OCBC、IBKR、老虎证券、富途、长桥等金融相关服务
  可选: 美国 / 日本 / DIRECT

🏠 国内服务
  默认: DIRECT
  用途: 国内服务、Apple/Microsoft 国内可直连部分、中国媒体、CN ASN、GEOIP CN

🌍 国际服务
  默认: 🇺🇸 美国节点
  用途: 代理媒体和通用国际代理规则

🌐 默认出口
  默认: 🇺🇸 美国节点
  用途: 所有未命中的兜底流量
```

## 出口节点筛选

```text
🇺🇸 美国节点
  类型: fallback
  筛选: 美国 / US / States / American 等关键词

🇯🇵 日本出口
  类型: fallback
  筛选: 日本 / JP / Japan 等关键词

🇸🇬 新加坡节点
  类型: fallback
  筛选: 新加坡 / 狮城 / SG / Singapore 等关键词
```

## 当前定向规则

```text
加密策略:
  Bybit 相关域名

金融策略:
  OCBC
  IBKR / Interactive Brokers
  老虎证券 / Tiger Brokers
  富途 / Futu / moomoo
  长桥 / Longbridge / LongPort / lbkrs

国内服务:
  Linear
  Wise / TransferWise
  Apple 部分服务
  香港虚拟银行相关域名
  Microsoft / Apple / App Store / ChinaMedia / ASN-CN 远程规则集
  GEOIP CN

国际服务:
  ProxyMedia 远程规则集
  Proxy 远程规则集
```

## 维护原则

```text
1. 特定服务优先写本地规则，避免被远程规则误分流。
2. 新加坡节点只表示出口节点池，不绑定具体业务场景。
3. 加密策略用于加密相关服务，默认走日本出口。
4. 默认出口保持美国，保证未命中流量优先可访问。
5. 增加新服务时，优先加 DOMAIN-SUFFIX，少用 DOMAIN-KEYWORD。
```
