# sites

一个静态导航站项目，用于集中展示常用网站、AI 工具、开发工具、实用工具、娱乐教育资源等入口。

项目通过 `index.html` 渲染界面，通过 `data.js` 维护站点数据，可直接静态部署。

## 项目结构

```text
sites/
├── index.html        # 页面结构、样式与交互逻辑
├── data.js           # 导航站数据源
├── leanengine.yaml   # LeanCloud / LeanEngine 静态部署配置
└── README.md
```

## 技术说明

- 纯静态 HTML / CSS / JavaScript
- 使用 CDN 引入 Tailwind CSS
- 不依赖打包工具
- 支持桌面端表格视图和移动端卡片视图

## 主要功能

- 顶部标签页切换不同页面分类
- 左侧类型导航快速定位到某类资源
- 桌面端表格展示名称、地址、备注、功能说明
- 移动端自动切换为卡片布局
- 点击地址可复制链接
- 功能列超出时悬浮显示完整内容

## 数据维护

站点数据存放在 [`data.js`](./data.js) 中，挂载在全局变量 `window.WEBPAGES_DATA` 下。

数据结构示意：

```js
window.WEBPAGES_DATA = {
  pages: {
    "AI工具": {
      "类型": [
        {
          "学习资源": [
            {
              "名称": "AI小课-视频",
              "地址": "https://example.com",
              "备注": "中国 | 直连 | 付费",
              "功能": "功能说明"
            }
          ]
        }
      ]
    }
  }
};
```

维护建议：

- 新增标签页：在 `pages` 下增加一个页面对象
- 新增分类：在某个页面的 `类型` 数组中增加一个分类对象
- 新增站点：在对应分类数组中追加一条记录
- 尽量保持字段名为 `名称`、`地址`、`备注`、`功能`

## 本地预览

因为是静态页面，直接用浏览器打开 [`index.html`](./index.html) 即可。

如果想用本地 HTTP 服务预览，可使用任意静态服务器，例如：

```bash
python -m http.server 8000
```

然后访问：

```text
http://localhost:8000
```

## 部署

项目包含 [`leanengine.yaml`](./leanengine.yaml)：

```yaml
runtime: static
staticPath: .
```

说明当前项目按静态站点方式部署，发布根目录即为当前目录。

除 LeanEngine 外，也可部署到任意静态托管平台，例如：

- Netlify
- Vercel
- GitHub Pages

## 修改说明

- 页面样式、布局、交互逻辑主要在 [`index.html`](./index.html)
- 站点内容主要在 [`data.js`](./data.js)
- 若要调整默认分类、导航行为、复制提示、移动端样式，优先修改 `index.html` 内嵌脚本与样式
