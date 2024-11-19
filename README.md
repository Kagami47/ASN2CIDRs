# ASN to CIDRs

该 Worker 脚本旨在处理请求并从 GitHub 仓库 `ipverse/asn-ip` 返回的 JSON 数据中提取基于提供的自治系统号（ASN）的 IPv4 和 IPv6 CIDR（无类别域间路由）。

## 安装

创建一个新的 Cloudflare Worker。然后，你可以把 `_worker.js` 的代码复制到你的 Worker 的脚本编辑器里。

## 使用

访问你的 Worker 的 URL，并在地址后面加上你想要查询的 ASN 号。
例如，如果你的 Worker 的网址是 `as.090227.xyz`，你可以访问：

- 直接访问 `as.090227.xyz`，你会得到当前访问的IP；
---
### 1. 返回 IPv4 的 CIDR
```url
https://as.090227.xyz/AS45102
```

这将返回 AS45102 的 IPv4 CIDR 列表。
```
5.181.224.0/23
8.208.0.0/16
8.209.0.0/19
8.209.36.0/22
8.209.40.0/21
8.209.48.0/20
8.209.64.0/18
...
```
---
### 2. 返回 IPv6 的 CIDR
```url
https://as.090227.xyz/AS45102?6
```

这将返回 AS45102 的 IPv4 CIDR 列表。
```
2400:3200::/48
2400:3200:baba::/48
2400:b200:4100::/46
2401:b180:4100::/48
2404:2280:1000::/36
2404:2280:2000::/35
2404:2280:4000::/36
2408:4000:1000::/48
2408:4009:500::/48
...
```
---
### 3. 返回所有格式的 CIDR
```url
https://as.090227.xyz/AS45102?4&6
或
https://as.090227.xyz/AS45102?all
```

这将返回 AS45102 的 IPv4 CIDR 列表。
```
5.181.224.0/23
8.208.0.0/16
8.209.0.0/19
8.209.36.0/22
8.209.40.0/21
8.209.48.0/20
8.209.64.0/18
2400:3200::/48
2400:3200:baba::/48
2400:b200:4100::/46
2401:b180:4100::/48
2404:2280:1000::/36
2404:2280:2000::/35
2404:2280:4000::/36
2408:4000:1000::/48
2408:4009:500::/48
...
```
---
### 4. 返回 CIDR 的 json
```url
https://as.090227.xyz/AS45102.json
```

这将返回 AS45102 的 json 内容。
```json
{
    "asn": 45102,
    "handle": "ALIBABA-CN-NET",
    "description": "Alibaba (US) Technology Co., Ltd.",
    "subnets": {
        "ipv4": [
            "5.181.224.0/23",
            "8.208.0.0/16",
            "8.209.0.0/19",
            "8.209.36.0/22",
            "8.209.40.0/21",
            "8.209.48.0/20",
            "8.209.64.0/18",
            "..."
        ],
        "ipv6": [
            "2400:3200::/48",
            "2400:3200:baba::/48",
            "2400:b200:4100::/46",
            "2401:b180:4100::/48",
            "2404:2280:1000::/36",
            "2404:2280:2000::/35",
            "2404:2280:4000::/36",
            "..."
        ]
    }
}
```

## 实际应用方式

你可以使用 `wget` 命令将结果保存到文件中：

```bash
wget -O ip.txt https://as.090227.xyz/AS45102
```

## 感谢

[ipverse](https://github.com/ipverse/asn-ip)