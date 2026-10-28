# 公网发布：GitHub Pages

网站发布目录为 `docs/`，入口为 `docs/index.html`。纯静态原型，无需安装依赖或构建。

## 首次开启

在仓库 Settings → Pages → Build and deployment 中：

1. Source 选择 Deploy from a branch。
2. Branch 选择 main，目录选择 /docs。
3. 点击 Save，等待 GitHub Pages 构建完成。

成功后使用 Pages 设置页显示的正式地址。默认地址预计为 https://huangbo1997.github.io/Africa-Dianping/ ，只有发布成功后才能访问。

如仓库套餐不支持当前私有仓库的 Pages，请先检查套餐，或选择支持私有仓库的静态托管；不要仅为发布而盲目变更仓库可见性。

## 更新

编辑 `prototype/index.html` 后，将内容同步到 `docs/index.html` 并推送 main，Pages 会自动发布。`docs` 中只放允许公开访问的静态文件。

该站点为虚构数据的交互原型，不接收真实支付，不保存用户信息。
