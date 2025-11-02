![BlessingWall-Vue](https://socialify.git.ci/QNquenan/BlessingWall-Vue/image?custom_description=%E4%B8%80%E4%B8%AA%E7%AE%80%E6%98%93%E7%9A%84%E7%A5%9D%E7%A6%8F%E5%A2%99&description=1&font=JetBrains+Mono&forks=1&issues=1&language=1&name=1&owner=1&pattern=Brick+Wall&pulls=1&stargazers=1&theme=Light)

# Blessing Wall 祝福墙

一个基于 Vue 3 和 Vite 构建的动态祝福墙应用，在页面上动态展示各种祝福语卡片。

## 项目简介

Blessing Wall（祝福墙）会在页面上动态生成带有祝福语的卡片，每张卡片都有随机的颜色、位置和旋转角度，营造出独特的视觉效果。主要页面是首页，会自动不断产生新的祝福卡片，并在屏幕上展示。

祝福语文本来自 [notes](https://github.com/uninto/notes/tree/main)

## 技术栈

- [Vue 3](https://v3.cn.vuejs.org/): 渐进式 JavaScript 框架
- [Vite](https://vitejs.dev/): 下一代前端构建工具
- [Vue Router](https://router.vuejs.org/): Vue.js 的官方路由管理器
- [motion-v](https://motion.vueuse.org/): Vue 的动画库
- [Less](http://lesscss.org/): CSS 预处理器

## 功能特性

- 🎋 响应式设计，适配多种设备
- 🎨 随机生成颜色的祝福卡片
- 🔄 自动动态添加新卡片
- ✨ 使用动画效果增强用户体验
- 📱 简洁直观的用户界面

## 快速开始

### 环境要求

- Node.js >= 20.19.0
- pnpm 包管理器

### 安装依赖

```bash
pnpm install
```

### 启动开发服务器

```bash
pnpm dev
```

默认情况下，应用将在 http://localhost:5173 上运行。

### 构建生产版本

```bash
pnpm build
```

构建产物将生成在 `dist` 目录中。

### 本地预览生产构建

```bash
pnpm preview
```

## 项目结构

```
.
├── src/
│   ├── assets/
│   │   └── config/
│   │       └── Blessing.json     # 祝福语配置文件
│   ├── components/
│   │   └── WindowsCard.vue       # 卡片组件
│   ├── pages/
│   │   ├── Home.vue              # 首页
│   │   └── Login.vue             # 登录页
│   ├── router/
│   │   └── index.js              # 路由配置
│   ├── App.vue                   # 根组件
│   └── main.js                   # 应用入口
├── public/
│   └── favicon.ico               # 网站图标
├── index.html                    # HTML 模板
└── vite.config.js                # Vite 配置文件
```

## 工作原理

1. 应用启动后进入首页 ([Home.vue](src/pages/Home.vue))
2. 从 [Blessing.json](src/assets/config/Blessing.json) 配置文件中读取祝福语列表
3. 初始化时创建5张卡片，并每300毫秒新增一张卡片
4. 当卡片数量超过100张时，移除最早创建的卡片
5. 每张卡片使用 [WindowsCard.vue](src/components/WindowsCard.vue) 组件渲染
6. 使用 [motion-v](https://motion.vueuse.org/) 库为卡片添加出现动画

## 自定义配置

### 修改祝福语

编辑 [src/assets/config/Blessing.json](src/assets/config/Blessing.json) 文件可以自定义祝福语：

```json
[
  "保持好心情",
  "多喝水哦",
  "今天辛苦啦",
  "早点休息"
]
```

### 调整卡片生成速度

可以在 [Home.vue](src/pages/Home.vue) 中调整卡片生成间隔时间：

```js
intervalId = setInterval(() => {
  cards.value.push(createRandomCard());
}, 300); // 修改这里的数值（单位：毫秒）
```

## 浏览器兼容性

由于使用了现代 Web API，建议在以下浏览器版本或更高版本中使用：

- Chrome 60+
- Firefox 60+
- Safari 12+
- Edge 79+

## 许可证

[MIT](LICENSE)
