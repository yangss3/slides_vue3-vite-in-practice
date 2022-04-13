---
theme: default
title: Vue3 + Vite 前端工程化实践
background: https://picsum.photos/1920/1080
layout: cover
class: 'text-center'
drawings:
  persist: false
---

# Vue3 + Vite 前端工程化实践

从零开始搭建一个基于 Vue3, Vite 和 TypeScript 的前端脚手架

杨书山

---

# 什么是前端工程化？

将开发阶段的代码发布到生产环境，包含：构建，分支管理，自动化测试，部署

提升前端开发效率、提高前端应用质量的方法和工具都是前端工程化

提升开发效率、提升产品质量、降低开发难度、降低企业成本应该是工程化的意义所在。

工程化划分了5部分：开发、构建、部署、性能、规范化


---

# Vue3 & Vite


<div class="grid grid-cols-2 gap-4">
<div>
<div v-click>

**安装 `vue` 和 `vite`**

```bash
npm install vue
npm install -D vite @vitejs/plugin-vue
```

</div>
<div v-click>

**VS Code 插件**

[TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.vscode-typescript-vue-plugin)

<!-- <a class="text-blue-400 hover:!text-blue-500" target="_blank" href="https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.vscode-typescript-vue-plugin">TypeScript Vue Plugin (Volar)</a> -->

</div>
</div>
<div v-click>

**创建 `vite.config.js`**

```js
import { defineConfig } from 'vite'
import Vue from '@vitejs/plugin-vue'

export default defineConfig({
  plugins: [Vue()]
})
```

</div>
<div v-click>

**初始化 Vue 应用 `src/main.js`**

```js
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```
</div>
<div v-click>

**入口文件 `index.html`**

```html
<body>
  <div id="app"></div>
  <script type="module" src="./src/main.js">
</body>
```
</div>
</div>

---

# 集成 TypeScript

<div class="grid grid-cols-2 gap-4 grid-rows-2">
  <!-- <div> -->
<div v-click>

**安装 TypeScript**
```bash
npm install -D typescript
```

</div>
<div v-click>

**创建 `tsconfig.json`**

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "lib": ["esnext", "dom"],
    "jsx": "preserve",
    "strict": true,
    "baseUrl": "./",
    "esModuleInterop": true,
    "skipLibCheck": true
  }
}
```

</div>
  <!-- </div> -->
</div>

---

# Script Setup

  <!-- **创建 `tsconfig.json`** -->
```json {all|2,4|3,5|6,8|all}
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "lib": ["esnext", "dom"],
    "jsx": "preserve",
    "strict": true,
    "baseUrl": "./",
    "esModuleInterop": true,
    "skipLibCheck": true
  }
}
```

---

# CSS 方案

```ts {2,3}
function add(
  a: Ref<number> | number,
  b: Ref<number> | number
) {
  return computed(() => unref(a) + unref(b))
}

```

---

# 组件自动导入

---

# API 自动导入


---

# 代码质量管理


---

# 路由和状态管理

---


# UI 组件库集成


---

# 单元测试

---

# 其它工具库推荐
