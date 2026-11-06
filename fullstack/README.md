# 前后端服务

Node.js 22.13+，无第三方依赖。客户端 `/`，管理端 `/admin`，SQLite 持久化。当前使用示例菜单，支付方式为到店付款。

## 本地启动（PowerShell）

在 fullstack 目录执行：

    $env:ADMIN_PASSWORD = Read-Host '设置管理员密码（至少12字符）'
    npm start

打开 http://localhost:3000 和 http://localhost:3000/admin 。密码不写入源码；生产环境必须通过部署平台设置 ADMIN_PASSWORD。运行 npm test 验证接口。

## 部署

GitHub Pages 不支持 Node 和数据库。完整服务必须部署到支持 Docker 和持久化磁盘的平台。已提供 Dockerfile 与 render.yaml；Render Blueprint 的文件路径选择 fullstack/render.yaml。该配置使用付费 starter 服务与1GB磁盘，需账户持有人自行确认套餐和费用后创建；本轮未购买或创建该服务。生成的管理员密码从平台环境变量页面查看。平台部署成功后使用返回的 HTTPS 域名访问客户端和 /admin。

也可在自有服务器运行 Docker，挂载 /data，设置 ADMIN_PASSWORD，并配置 HTTPS 反向代理。备份 /data/store.sqlite 及 WAL 文件时应停止写入或使用 SQLite 备份工具。单实例部署，不能使用多个各有独立磁盘的副本。

## 已实现

菜单接口、规格加料、购物车、堂食桌号/自取、电话校验、服务器计算金额、订单行价格快照、幂等下单、凭随机令牌查询订单；员工密码登录、HttpOnly 会话、订单状态约束、商品新增/编辑/售罄、登录限流、同源与 CSP 保护。

接口：GET /api/menu；POST /api/orders；GET /api/orders/:id（X-Order-Token）；POST /api/admin/login；POST /api/admin/logout；GET /api/admin/orders；PATCH /api/admin/orders/:id；POST /api/admin/products。

## 验证与边界

接口集成测试覆盖登录拒绝、权限保护、服务端计价、防重复下单、订单凭证、状态约束与售罄拦截；尚未完成浏览器交互验证。当前为单门店 MVP，未接入支付、配送、短信、打印和多员工角色。示例菜单必须在营业前替换并核实门店信息。订单查询令牌仅保存在当前页内存，关闭页面前需要保持页面用于跟踪。
