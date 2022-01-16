V2Ray 基于 Nginx 的 vless+ws+tls 一键安装脚本

感谢wulabing的脚本

关于 VMess MD5 认证信息 淘汰机制
自 2022 年 1 月 1 日起，服务器端将默认禁用对于 MD5 认证信息 的兼容。任何使用 MD5 认证信息的客户端将无法连接到禁用 VMess MD5 认证信息的服务器端。
受到影响的用户，我们强烈建议您重新安装，并设置alterid为0（默认值目前已经修改为0），不再使用 VMess MD5 认证机制 如果您不想重新安装，您可以通过使用 https://github.com/KukiSa/VMess-fAEAD-disable 强制开启对于 MD5 认证机制的兼容

准备工作

准备一个域名，并将A记录添加好。
V2ray官方说明，了解 TLS WebSocket 及 V2ray 相关信息

安装好 wget

安装/更新方式
Vless+websocket+TLS+Nginx+Website

wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/tooiiby/V2Ray_ws-tls/main/install.sh" && chmod +x install.sh && bash install.sh

注意事项

如果你不了解脚本中各项设置的具体含义，除域名外，请使用脚本提供的默认值
使用本脚本需要你拥有 Linux 基础及使用经验，了解计算机网络部分知识，计算机基础操作
目前支持Debian 9+ / Ubuntu 18.04+ / Centos7+ ，部分Centos模板可能存在难以处理的编译问题，建议遇到编译问题时，请更换至其他系统模板
群主仅提供极其有限的支持，如有问题可以询问群友
每周日的凌晨3点，Nginx 会自动重启以配合证书的签发定时任务进行，在此期间，节点无法正常连接，预计持续时间为若干秒至两分钟

查看客户端配置
cat ~/v2ray_info.txt

V2ray 简介

V2Ray是一个优秀的开源网络代理工具，可以帮助你畅爽体验互联网，目前已经全平台支持Windows、Mac、Android、IOS、Linux等操作系统的使用。
本脚本为一键完全配置脚本，在所有流程正常运行完毕后，直接按照输出结果设置客户端即可使用
请注意：我们依然强烈建议你全方面的了解整个程序的工作流程及原理
建议单服务器仅搭建单个代理

本脚本默认安装最新版本的V2ray core（同时请注意客户端 core 的同步更新，需要保证客户端内核版本 >= 服务端内核版本）
建议使用默认的443端口作为连接端口
伪装内容可自行替换。

注意事项
推荐在纯净环境下使用本脚本，如果你是新手，请不要使用Centos系统。
在尝试本脚本确实可用之前，请不要将本程序应用于生产环境中。
该程序依赖 Nginx 实现相关功能，请使用 LNMP 或其他类似携带 Nginx 脚本安装过 Nginx 的用户特别留意，使用本脚本可能会导致无法预知的错误（未测试，若存在，后续版本可能会处理本问题）。
V2Ray 的部分功能依赖于系统时间，请确保您使用V2RAY程序的系统 UTC 时间误差在三分钟之内，时区无关。
本 bash 依赖于 V2ray 官方安装脚本 及 acme.sh 工作。

Centos 系统用户请预先在防火墙中放行程序相关端口（默认：80，443）

启动方式

启动 V2ray：systemctl start v2ray

停止 V2ray：systemctl stop v2ray

启动 Nginx：systemctl start nginx

停止 Nginx：systemctl stop nginx

相关目录

Web 目录：/home/wwwroot/catch-the-cat

V2ray 服务端配置：/etc/v2ray/config.json

V2ray 客户端配置: ~/v2ray_info.inf

Nginx 目录： /etc/nginx

证书文件: /data/v2ray.key 和 /data/v2ray.crt 请注意证书权限设置
