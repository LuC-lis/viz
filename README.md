# Viz

独立的交互式 HTML 可视化托管站，通过 GitHub Pages 发布，用来给 Notion 等文档工具做 `embed`（iframe）嵌入。

线上地址：<https://luc-lis.github.io/viz/>

## 为什么单独开一个仓库

Notion 的 `/embed` 块需要一个**公网、稳定、允许被 iframe 嵌入**的地址：

- 上传到 Notion 自己存储的 HTML 文件只有一条 1 小时有效的预签名 S3 链接，过期即 403；
- Notion 3.6 的 `/html` 块虽然会执行上传的 HTML，但沙箱**禁止一切网络请求**，从 CDN 加载 Plotly / ECharts / 字体都会失败。

放到 GitHub Pages 上两个问题都没有：地址永久，网络正常，且 Pages 不发送 `X-Frame-Options`。

## 新增一个可视化

```bash
cp /path/to/widget.html ~/repos/viz/widget.html
# 在 index.html 的 <ul> 里加一张卡片
git add . && git commit -m "add widget" && git push
```

然后在 Notion 里输入 `/embed`，粘贴 `https://luc-lis.github.io/viz/widget.html`。

## 约定

- 每个页面都是**单文件**、自包含（样式和脚本写在文件内，第三方库可以用 CDN）；
- 页面背景不要透明，Notion 里明暗主题由页面自己决定；
- 内容自动刷新延迟：Pages 构建约 1 分钟。

## 现有页面

| 文件 | 内容 |
| --- | --- |
| `canyon.html` | 病态二次函数 `f(x,y)=0.5(10x²+y²)` 上的 SGD 收敛过程（Plotly 3D 曲面 + 轨迹） |
| `gradient-descent.html` | 一维双井函数 `f(x)=x⁴/4−x²/2` 的梯度下降：切线、负梯度箭头、收敛轨迹，可调 η / x₀，点画布直接换起点 |
