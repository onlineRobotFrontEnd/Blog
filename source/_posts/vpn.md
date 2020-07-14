---
title: VPN
date: 2020-6-28
author: zhangzhihui
category: VPN V2Ray
tags:
- VPN, V2Ray
---

## V2Ray是什么

V2Ray 是一个网络转发程序，支持 TCP、mKCP、WebSocket 这3种底层传输协议，支持 HTTP、Socks、Shadowsocks、VMess 这4种内容传输协议（HTTP只支持传入），并且有完整的 TLS 实现，是一个非常强大的平台。

### 简介

V2Ray官网：[https://www.v2ray.com](https://www.v2ray.com)

### ProjectV

Project V 是一个工具集合，它可以帮助你打造专属的基础通信网络。Project V 的核心工具称为 V2Ray，其主要负责网络协议和功能的实现，与其它 Project V 通信。V2Ray 可以单独运行，也可以和其它工具配合，以提供简便的操作流程。

特性：

- 多入口多出口: 一个 V2Ray 进程可并发支持多个入站和出站协议，每个协议可独立工作。
- 可定制化路由: 入站流量可按配置由不同的出口发出。轻松实现按区域或按域名分流，以达到最优的网络性能。
- 多协议支持: V2Ray 可同时开启多个协议支持，包括 Socks、HTTP、Shadowsocks、VMess 等。每个协议可单独设置传输载体，比如 TCP、mKCP、WebSocket 等。
- 隐蔽性: V2Ray 的节点可以伪装成正常的网站（HTTPS），将其流量与正常的网页流量混淆，以避开第三方干扰。
- 反向代理: 通用的反向代理支持，可实现内网穿透功能。
- 多平台支持: 原生支持所有常见平台，如 Windows、Mac OS、Linux，并已有第三方支持移动平台。

#### Shadowsocks

Shadowsocks 协议，包含入站和出站两部分，兼容大部分其它版本的实现。

与官方版本的兼容性：

- 支持 TCP 和 UDP 数据包转发，其中 UDP 可选择性关闭；
- 支持 OTA；
  - 客户端可选开启或关闭；
  - 服务器端可强制开启、关闭或自适应；
- 加密方式（其中 AEAD 加密方式在 V2Ray 3.0 中加入）：
  - aes-256-cfb
  - aes-128-cfb
  - chacha20
  - chacha20-ietf
  - aes-256-gcm
  - aes-128-gcm
  - chacha20-poly1305 或称 chacha20-ietf-poly1305
- 插件：
  - 通过 Standalone 模式支持 obfs

Shadowsocks 的配置分为两部分，InboundConfigurationObject和OutboundConfigurationObject，分别对应入站和出站协议配置中的settings项。

***InboundConfigurationObject***

```json
{
  "email": "love@v2ray.com", // 邮件地址，可选，用于标识用户
  "method": "aes-128-cfb", // 加密方式，可选如上所示
  "password": "密码", // 必填，任意字符串。Shadowsocks 协议不限制密码长度，但短密码会更可能被破解，建议使用 16 字符或更长的密码。
  "level": 0, // 用户等级，默认为0
  "ota": true, // 是否强制 OTA，如果不指定此项，则自动判断。强制开启 OTA 后，V2Ray 会拒绝未启用 OTA 的连接。反之亦然。
  "network": "tcp" // 可接收的网络连接类型，默认值为"tcp"。 可选值："tcp" | "udp" | "tcp,udp"
}
```

***OutboundConfigurationObject***

```json
{
  "servers": [ // 一个数组，其中每一项是一个 ServerObject。
    {
      "email": "love@v2ray.com", // 邮件地址，可选，用于标识用户
      "address": "127.0.0.1", // Shadowsocks 服务器地址，支持 IPv4、IPv6 和域名。必填。
      "port": 1234, // Shadowsocks 服务器端口。必填。
      "method": "加密方式", // 必填。可选的值见加密方式列表
      "password": "密码", // 必填。任意字符串。Shadowsocks 协议不限制密码长度，但短密码会更可能被破解，建议使用 16 字符或更长的密码。
      "ota": false, // 是否开启 Shadowsocks 的一次验证（One time auth），默认值为false。
      "level": 0 // 用户等级
    }
  ]
}
```

#### VMess

VMess 是一个加密传输协议，它分为入站和出站两部分，通常作为 V2Ray 客户端和服务器之间的桥梁。

VMess 依赖于系统时间，请确保使用 V2Ray 的系统 UTC 时间误差在 90 秒之内，时区无关。在 Linux 系统中可以安装ntp服务来自动同步系统时间。

VMess 的配置分为两部分，InboundConfigurationObject和OutboundConfigurationObject，分别对应入站和出站协议配置中的settings项。

***InboundConfigurationObject***

```json
{
  "clients": [
    {
      "id": "27848739-7e62-4138-9fd3-098a63964b6b",
      "level": 0,
      "alterId": 4,
      "email": "love@v2ray.com"
    }
  ],
  "default": {
    "level": 0,
    "alterId": 4
  },
  "detour": {
    "to": "tag_to_detour"
  },
  "disableInsecureEncryption": false
}
```

其中：

- clients: 一组服务器认可的用户。clients 可以为空。当此配置用作动态端口时，V2Ray 会自动创建用户。
  - id: VMess 的用户 ID。必须是一个合法的 UUID。
  - level: 用户等级，详情见[V2ray本地策略](https://www.v2ray.com/chapter_02/policy.html)
  - alterId: 为了进一步防止被探测，一个用户可以在主 ID 的基础上，再额外生成多个 ID。这里只需要指定额外的 ID 的数量，推荐值为 4。不指定的话，默认值是 0。最大值 65535。这个值不能超过服务器端所指定的值。
  - email: 用户邮箱地址，用于区分不同用户的流量。
- detour: 指示对应的出站协议使用另一个服务器。
  - to: 一个入站协议的tag，详见[V2ray配置文件](https://www.v2ray.com/chapter_02/02_protocols.html)。指定的入站协议必须是一个 VMess
- default: 可选，clients 的默认配置。仅在配合detour时有效。
- disableInsecureEncryption: 是否禁止客户端使用不安全的加密方式，当客户端指定下列加密方式时，服务器会主动断开连接。默认值为false。
  - "none"
  - "aes-128-cfb"

***OutboundConfigurationObject***

```json
{
  "vnext": [
    {
      "address": "127.0.0.1",
      "port": 37192,
      "users": [
        {
          "id": "27848739-7e62-4138-9fd3-098a63964b6b",
          "alterId": 4,
          "security": "auto",
          "level": 0
        }
      ]
    }
  ]
}
```

其中：

- vnext表示服务器配置
  - address: 地址
  - port: 端口
  - users: 用户信息
    - id: VMess 用户的主 ID。必须是一个合法的 UUID。
    - alterId: 为了进一步防止被探测，一个用户可以在主 ID 的基础上，再额外生成多个 ID。这里只需要指定额外的 ID 的数量，推荐值为 4。不指定的话，默认值是 0。最大值 65535。这个值不能超过服务器端所指定的值。
    - level: 用户等级
    - security: 加密方式，客户端将使用配置的加密方式发送数据，服务器端自动识别，无需配置。
      - "aes-128-gcm"：推荐在 PC 上使用
      - "chacha20-poly1305"：推荐在手机端使用
      - "auto"：默认值，自动选择（运行框架为 AMD64、ARM64 或 s390x 时为aes-128-gcm加密方式，其他情况则为 Chacha20-Poly1305 加密方式）
      - "none"：不加密
      - `推荐使用"auto"加密方式，这样可以永久保证安全性和兼容性。`

## 安装流程

### 1.购买VPS

任何境外 VPS 都可以，一般而言香港、台湾、新加坡、韩国、日本等亚洲机房速度（延迟小）最快，但价格较贵，并且由于用的人多经常会被重点关照。无论如何，如果预算充足并追求速度可以选择这些机房，但需要提前了解测试线路是否是直连中国，一些线路可能会绕美国。

美国VPS价格低廉宽带足，其中的洛杉矶(Los Angeles)、西雅图(Seattle)两个机房对中国物理距离最近，这两个机房为首选。

推荐[VirMach](https://virmach.com/),便宜的1.25刀一个月，一次性买10个月，送两个月

```text
256MB DEDICATED RAM
1 vCORE
10GB SSD (HW RAID 10)
DDoS Protection Available
500GB BANDWIDTH
1GBPS
```

服务器可以配置为Ubuntu或者CenterOS,看个人喜好

使用终端ssh登录

### 2.安装V2Ray

V2Ray 提供了一个在 Linux 中的自动化安装脚本。这个脚本会自动检测有没有安装过 V2Ray，如果没有，则进行完整的安装和配置；如果之前安装过 V2Ray，则只更新 V2Ray 二进制程序而不更新配置。

以下指令假设已在 su 环境下，如果不是，请先运行 sudo su。

运行下面的指令下载并安装 V2Ray。当 yum 或 apt-get 可用的情况下，此脚本会自动安装 unzip 和 daemon。这两个组件是安装 V2Ray 的必要组件。如果你使用的系统不支持 yum 或 apt-get，请自行安装 unzip 和 daemon

可能需要安装curl，unzip，git等工具

```bash
sudo -i
bash <(curl -s -L https://git.io/v2ray.sh)
```

- 然后选择安装，即是输入 1 回车;
- 选择传输协议，如果没有特别的需求，使用默认的 TCP 传输协议即可，直接回车;
- 选择端口，如果没有特别的需求，使用默认的端口即可，直接回车;
- 是否屏蔽广告，除非你真的需要，一般来说，直接回车即可;
- 是否配置 Shadowsocks ，如果不需要就直接回车，否则就输入 Y 回车;
- Shadowsocks 端口，密码，加密方式这些东西自己看情况配置即可，一般全部直接回车。
OK，按回车继续;
- 最后安装完成后会提示安装信息，建议记录下。

此脚本会自动安装以下文件：

- /usr/bin/v2ray/v2ray：V2Ray 程序；
- /usr/bin/v2ray/v2ctl：V2Ray 工具；
- /etc/v2ray/config.json：配置文件；
- /usr/bin/v2ray/geoip.dat：IP 数据文件
- /usr/bin/v2ray/geosite.dat：域名数据文件

此脚本会配置自动运行脚本。自动运行脚本会在系统重启之后，自动运行 V2Ray。目前自动运行脚本只支持带有 Systemd 的系统，以及 Debian / Ubuntu 全系列。

运行脚本位于系统的以下位置：

- /etc/systemd/system/v2ray.service: Systemd
- /etc/init.d/v2ray: SysV

脚本运行完成后，你需要：

编辑 /etc/v2ray/config.json 文件来配置你需要的代理方式；

config.json配置如下所示：

```json
{
  "inbounds": [{
    "port": 10086, // 服务器监听端口，必须和上面的一样
    "protocol": "vmess",
    "settings": {
      "clients": [{ "id": "b831381d-6324-4d53-ad4f-8cda48b30811" }]
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  }]
}
```

运行 service v2ray start 来启动 V2Ray 进程；
之后可以使用 service v2ray start|stop|status|reload|restart|force-reload 控制 V2Ray 的运行。

客户端配置信息(PC,iphone)：

```json
{
  "inbounds": [{
    "port": 1080,  // SOCKS 代理端口，在浏览器中需配置代理并指向这个端口
    "listen": "127.0.0.1",
    "protocol": "socks",
    "settings": {
      "udp": true
    }
  }],
  "outbounds": [{
    "protocol": "vmess",
    "settings": {
      "vnext": [{
        "address": "server", // 服务器地址，请修改为你自己的服务器 ip 或域名
        "port": 10086,  // 服务器端口
        "users": [{ "id": "b831381d-6324-4d53-ad4f-8cda48b30811" }]
      }]
    }
  },{
    "protocol": "freedom",
    "tag": "direct",
    "settings": {}
  }],
  "routing": {
    "domainStrategy": "IPOnDemand",
    "rules": [{
      "type": "field",
      "ip": ["geoip:private"],
      "outboundTag": "direct"
    }]
  }
}
```

开放响应端口：[CenterOS7开放响应端口](https://www.4spaces.org/centos-open-porter/)

V2Ray常用命令

- `v2ray info`：查看 V2Ray 配置信息
- `v2ray config`：修改 V2Ray 配置
- `v2ray link`：生成 V2Ray 配置文件链接
- `v2ray infolink`：生成 V2Ray 配置信息链接
- `v2ray qr`：生成 V2Ray 配置二维码链接
- `v2ray ss`：修改 Shadowsocks 配置
- `v2ray ssinfo`：查看 Shadowsocks 配置信息
- `v2ray ssqr`：生成 Shadowsocks 配置二维码链接
- `v2ray status`：查看 V2Ray 运行状态
- `v2ray start`：启动 V2Ray
- `v2ray stop`：停止 V2Ray
- `v2ray restart`:重启 V2Ray
- `v2ray log`：查看 V2Ray 运行日志
- `v2ray update`：更新 V2Ray
- `v2ray update.sh`：更新 V2Ray 管理脚本
- `v2ray uninstall`：卸载 V2Ray

### [神一样的工具](https://www.v2ray.com/awesome/tools.html)

V2RayW

V2RayW 是一个基于 V2Ray 内核的 Windows 客户端。用户可以通过界面生成配置文件，并且可以手动更新 V2Ray 内核。下载：[GitHub](https://github.com/Cenmrev/V2RayW)

V2RayN

V2RayN 是一个基于 V2Ray 内核的 Windows 客户端。下载：[GitHub](https://github.com/2dust/v2rayN)

Clash for Windows

下载：[GitHub](https://github.com/Fndroid/clash_for_windows_pkg)

V2RayX

V2RayX 是一个基于 V2Ray 内核的 Mac OS X 客户端。用户可以通过界面生成配置文件，并且可以手动更新 V2Ray 内核。V2RayX 还可以配置系统代理。下载：[Github](https://github.com/Cenmrev/V2RayX)

V2RayU

V2rayU,基于v2ray核心的mac版客户端,界面友好,使用swift4.2编写,支持vmess,shadowsocks,socks5等服务协议,支持订阅, 支持二维码,剪贴板导入,手动配置,二维码分享等。下载：[GitHub](https://github.com/yanue/V2rayU)

V2RayC

下载：[GitHub](https://github.com/gssdromen/V2RayC)

ClashX

下载：[GitHub](https://github.com/yichengchen/clashX)

Qv2ray

Qv2ray：使用 Qt 编写的 v2ray 跨平台 GUI （MacOS, Windows, Linux）支持连接导入和编辑，中英文切换

下载：[GitHub](https://github.com/lhy0403/Qv2ray)

官网：[https://lhy0403.github.io/Qv2ray](https://lhy0403.github.io/Qv2ray)

Mellow

Mellow 是一个基于规则的全局透明代理工具，可以运行在 Windows、macOS 和 Linux 上，也可以配置成路由器透明代理或代理网关，支持 SOCKS、HTTP、Shadowsocks、VMess 等多种代理协议。

Download: [Github](https://github.com/mellow-io/mellow)

Kitsunebi  

Kitsunebi 是一个基于 V2Ray 核心的移动平台应用 (iOS, Android)。它可以创建基于 VMess 或者 Shadowsocks 的 VPN 连接。Kitsunebi 支持导入和导出与 V2Ray 兼容的 JSON 配置。

由于使用 V2Ray 核心，Kitsunebi 几乎支持 V2Ray 的所有功能，比如 Mux 和 mKCP。

下载：[iTunes](https://itunes.apple.com/us/app/kitsunebi-proxy-utility/id1446584073?mt=8) | [Play Store](https://play.google.com/store/apps/details?id=fun.kitsunebi.kitsunebi4android&hl=en_US)

i2Ray

i2Ray 是另一款基于 V2Ray 核心的iOS应用。界面简洁易用，适合新手用户使用。同时兼容Shadowrocket和Quantumult格式的规则导入。

下载：[iTunes](https://itunes.apple.com/us/app/i2ray/id1445270056?mt=8)

Shadowrocket

Shadowrocket 是一个通用的 iOS VPN 应用，它支持众多协议，如 Shadowsocks、VMess、SSR 等。

下载：[iTunes](https://itunes.apple.com/us/app/shadowrocket/id932747118?mt=8)

Pepi（原名ShadowRay）

Pepi 是一个兼容 V2Ray 的 iOS 应用，它可以创建基于 VMess 的 VPN 连接，并与 V2Ray 服务器通信。

下载：[iTunes](https://itunes.apple.com/us/app/pepi/id1283082051?mt=8)

Quantumult

下载：[iTunes](https://itunes.apple.com/us/app/quantumult/id1252015438?mt=8)

BifrostV

BifrostV 是一个基于 V2Ray 内核的 Android 应用，它支持 VMess、Shadowsocks、Socks 协议。

下载：[Play Store](https://play.google.com/store/apps/details?id=com.github.dawndiy.bifrostv)

V2RayNG

V2RayNG 是一个基于 V2Ray 内核的 Android 应用，它可以创建基于 VMess 的 VPN 连接。

下载：[GitHub](https://github.com/2dust/v2rayNG)

在线工具/资源

VeekXT V2Ray配置生成

支持 4.x 版本的配置文件生成器 [veekxt.com](https://www.veekxt.com/utils/v2ray_gen)

V2Ray 配置生成器

静态 V2Ray 配置文件生成页面 [GitHub](https://github.com/htfy96/v2ray-config-gen)

UUID Generator

VMess User ID 生成工具 [uuidgenerator.net](https://www.uuidgenerator.net/)

vTemplate 项目仓库

一个 V2Ray 配置文件模板收集仓库 [GitHub](https://github.com/KiriKira/vTemplate)

### 3.Cloudflare中转V2Ray Websocket流量

首先需要一个域名，可以通过[freenom](http://freenom.com/zh/index.html)来获取免费使用一年的域名。

注册[Cloudflare](https://cloudflare.com)，添加DNS记录，

然后在freenom上面[配置Nameservers](https://my.freenom.com/clientarea.php?action=domaindetails&id=1094581177#tab3)

可参考教程：[使用Cloudflare+WebSocket+TLS+Nginx搭建V2ray拯救被封国外VPS 脚本已可用](https://www.wervps.com/we/2541.html)

[V2Ray 基于 Nginx 的 vmess+ws+tls 一键安装脚本](https://github.com/wulabing/V2Ray_ws-tls_bash_onekey)

## 国内外网站分享

- 翻墙必去

[www.google.com](www.google.com),这个就不多说了

- [Instagram](https://www.instagram.com/?hl=en)，[Twitter](https://twitter.com/)

- 程序员网站：

国外： [https://stackoverflow.com/](https://stackoverflow.com/)

国内： [掘金](https://juejin.im/)，[思否](https://segmentfault.com/)

- 刷题网站

[力扣](https://leetcode-cn.com/), [CodeWars](https://www.codewars.com/)

- [AirPano](https://www.airpano.com/360photo_list.php)-不出门看遍全球风景

- 图片压缩

[TinyJPG](https://tinyjpg.com/),[TinyPNG](https://tinypng.com/)

- HTML颜色

[html-color-codes](https://html-color-codes.info/chinese/)

- 字体图标库

[http://fontello.com/](http://fontello.com/), [ICONSVG](https://iconsvg.xyz/)

ICONSVG 支持导出SVG,jsx和React代码，可直接使用

```jsx
import React from "react";
const MapMarker3 = ({size=24, color="#000000"}) => (<svg xmlns="http://www.w3.org/2000/svg" width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><circle cx="11.5" cy="8.5" r="5.5"/><path d="M11.5 14v7"/></svg>);
export default MapMarker3;
```

参考文章： [V2Ray完全使用教程](https://yuan.ga/v2ray-complete-tutorial/), [V2Ray 搭建教程以及一键安装脚本](https://www.imtqy.com/amp/v2ray.html),
