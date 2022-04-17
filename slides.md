---
theme: default
title: Vue3 + Vite 前端工程化实践
background: https://picsum.photos/1920/1080
layout: cover
class: 'text-center'
highlighter: shiki
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

从一个最简单的 Vue3 应用开始

<div class="grid grid-cols-2 gap-6">
<div v-click>

**安装 `vue` 和 `vite`**

```bash
npm install vue
npm install -D vite @vitejs/plugin-vue
```

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

# TypeScript 集成

Vite 提供了开箱即用的 TypeScript 支持

<div class="grid grid-cols-2 gap-6">
<div>
<div v-click>

**安装 TypeScript**
```bash
npm install -D typescript
```

</div>
<div v-click class="mt-40px">

**VS Code 插件**

[Vue Language Features (Volar)](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar)

</div>
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
    "esModuleInterop": true,
    "skipLibCheck": true,
    "baseUrl": "./",
  }
}
```

</div>
</div>

---

# CSS 方案

CSS 预处理器 / PostCSS Preset Env

<STwoCols class="-mt-4">
<div v-click>

**Vite 提供了开箱即用的 CSS 预处理器支持**

```bash
# .scss/.sass
npm install -D sass

# .less
npm install -D less

# .styl/.stylus
npm install -D stylus
```

</div>

<div v-click>

<p class="font-bold">写标准的现代 CSS - <a target="_blank" href="https://preset-env.cssdb.org/">PostCSS Preset Env</a>
<SBadge>推荐</SBadge>
</p>

安装 `postcss-preset-env`：
```bash
npm install -D postcss-preset-env
```
配置 `vite.config.ts`：
```ts
import { defineConfig } from 'vite'
import PostCSSPresetEnv from 'postcss-preset-env'

export default defineConfig({
  css: {
    postcss: {
      plugins: [PostCSSPresetEnv({ stage: 1 })]
    }
  }
})
```

</div>
</STwoCols>

<!--
https://github.com/csstools/postcss-plugins/tree/main/plugin-packs/postcss-preset-env

PostCSS Preset Env lets you convert modern CSS into something most browsers can understand, determining the polyfills you need based on your targeted browsers or runtime environments.
 -->

---

# CSS 方案

最流行的原子 CSS 框架：[Tailwind CSS](https://tailwindcss.com/) / [Windi CSS](https://windicss.org/)

<div v-click="1" class="flex items-center gap-x-4">

```html
<button class="py-1 px-4 rounded text-white bg-blue-400 active:bg-blue-500">CLICK</Button>
```

<button class="py-1 px-4 rounded text-white bg-blue-400 active:bg-blue-500">CLICK</Button>

</div>


<div class="flex items-center">

<div v-click="2" class="flex items-center">

**安装：**
```bash
npm install -D windicss vite-plugin-windicss
```

</div>
<div v-click="5" class="ml-60px">

**VS Code 插件：[Windi CSS Intellisense](https://marketplace.visualstudio.com/items?itemName=voorjaar.windicss-intellisense)**

</div>

</div>
<STwoCols>
<div v-click="3">

```ts
// vite.config.ts
import { defineConfig } from 'vite'
import WindiCSS from 'vite-plugin-windicss'

export default defineConfig({
  plugins: [
    WindiCSS()
  ]
})

// main.ts
import 'virtual:windi.css'
```

</div>
<div v-click="4">

`windi.config.ts`：
```ts
import { defineConfig } from 'windicss/helpers'

export default defineConfig({
  extract: {
    include: ['src/**/*.{vue,html,ts,tsx}'],
    exclude: ['node_modules', '.git']
  }
})
```

</div>
</STwoCols>

---

# 前端路由 - Vue Router 4.x

基于组合式 API 的路由库

<STwoCols class="two-cols">
<div>

<div v-click>

创建路由：

```ts
// router.ts
import {
  createRouter,
  createWebHistory
} from 'vue-router'

export default createRouter({
  history: createWebHistory(),
  routes: [ /* ... */ ]
})
```

</div>
<div v-click>

注册路由：

```ts
// main.ts
import router from './router'
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).use(router).mount('#app')
```

</div>
</div>
<div v-click>

使用路由：

```html
<script lang="ts">
import { defineComponent } from 'vue'
import { useRouter, useRoute } from 'vue-router'

export default defineComponent({
  setup() {
    const router = useRouter()
    const route = useRoute()
    return { router, route }
  }
})
</script>

<template>
  <p>{{ route.name }}</p>
  <button @click="router.push('/about')">About</button>
</template>
```

</div>
</STwoCols>

<style>
.two-cols { @apply -mt-10px; }
.two-cols p { @apply !mt-1 !mb-1; }
</style>

---

# 全局状态管理 - [Pinia](https://pinia.vuejs.org/)

官方推荐的下一代状态管理库

<STwoCols class="two-cols">
<div>

<div v-click>

安装 pinia:
```ts
// main.ts
import { createPinia } from 'pinia'
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).use(createPinia()).mount('#app')
```

</div>

<div v-click>

定义一个 store：

```ts
// store/counter.ts
import { defineStore } from 'pinia'
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0 }),
  actions: {
    increment() {
      this.count++
    }
  }
})
```

</div>
</div>
<div v-click>

使用 store：

```html
<script lang="ts">
import { defineComponent } from 'vue'
import { useCounterStore } from './store/counter'

export default defineComponent({
  setup() {
    const counterStore = useCounterStore()
    return { counterStore }
  }
})
</script>

<template>
  <button @click="counterStore.increment">
    {{ counterStore.count }}
  </button>
</template>
```

</div>
</STwoCols>

<style>
.two-cols { @apply -mt-10px; }
.two-cols p { @apply !mt-1 !mb-1; }
</style>

---

# Script Setup

编译时语法糖，简化 SFC 的代码编写

<div v-click>

```html
<template>
  <HelloWorld />
  <button @click="increment">{{ count }}</button>
</template>
```

</div>

<div class="grid grid-cols-[1fr,70px,1fr] gap-3">
<div v-click>

```html
<script lang="ts">
import { ref, defineComponent } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

export default defineComponent({
  components: { HelloWorld },
  setup() {
    const count = ref(0)
    function increment() {
      count.value++
    }
    return { count, increment }
  }
})
</script>
```

</div>
<div v-click class="relative">
  <span class="absolute top-24 left-0.5 text-xs">script setup</span>
  <arrow x1="0" y1="120" x2="70" y2="120" color="gray" width="1" arrowSize="1" />
</div>

<div v-after class="setup">

```html
<script setup lang="ts">
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const count = ref(0)
function increment() {
  count.value++
}
</script>
```

</div>
</div>

<style>
.setup .slidev-code .line:first-child span:nth-child(4){
  @apply font-bold !text-blue-500;
}
</style>

---

# 组件自动导入

自动按需导入和注册组件：`unplugin-vue-components`

<STwoCols>
<div>
<div v-click>

```html
<script setup>
import HelloWorld from './components/HelloWorld.vue'
import Foo from './components/Foo.vue'
import Bar from './components/Bar.vue'
</script>

<template>
  <HelloWorld />
  <Foo />
  <Bar />
</template>
```

</div>
<div v-click class="relative">
  <arrow class="relative h-40px" x1="150" y1="0" x2="150" y2="40" color="gray" width="1" arrowSize="1" />
  <span class="absolute top-2 left-160px text-sm">自动导入组件</span>
</div>
<div v-after>

```html
<template>
  <HelloWorld />
  <Foo />
  <Bar />
</template>
```

</div>
</div>
<div>
<div v-click>

**安装 `unplugin-vue-components`**：
```bash
npm install -D unplugin-vue-components
```

</div>
<div v-click>

`vite.config.ts`：

```ts
import { defineConfig } from 'vite'
import Components from 'unplugin-vue-components/vite'

export default defineConfig({
  plugins: [
    Components()
  ]
})
```

</div>
</div>


</STwoCols>


---

# API 自动导入

自动按需导入 API：`unplugin-auto-import`

<STwoCols>
<div>
<div v-click>

```ts
import { computed, ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const count = ref(0)
const doubled = computed(() => count.value * 2)
const router = useRouter()
const route = useRoute()
```

</div>
<div v-click class="relative">
  <arrow class="relative h-40px" x1="150" y1="0" x2="150" y2="40" color="gray" width="1" arrowSize="1" />
  <span class="absolute top-2 left-160px text-sm">自动导入 API</span>
</div>
<div v-after>

```ts
const count = ref(0)
const doubled = computed(() => count.value * 2)
const router = useRouter()
const route = useRoute()
```

</div>
</div>
<div>
<div v-click>

**安装 `unplugin-auto-import`**：
```bash
npm install -D unplugin-auto-import
```

</div>
<div v-click>

`vite.config.ts`：

```ts
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'

export default defineConfig({
  plugins: [
    AutoImport({
      imports: ['vue', 'vue-router']
    })
  ]
})
```

</div>
</div>


</STwoCols>

---

# UI 组件库集成

[Ant Design Vue 3.x](https://www.antdv.com/docs/vue/introduce-cn) / [Element Plus](https://element-plus.gitee.io/zh-CN/)

<STwoCols>
<div v-click>

**安装 Ant Design Vue:**
```bash
npm install ant-design-vue
```
```ts
// main.ts
import { createApp } from 'vue'
import App from './App'
import Antd from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css'

const app = createApp(App)
app.use(Antd).mount('#app')
```

</div>
<div v-click>

**按需自动导入组件**

```ts
import { defineConfig } from 'vite'
import Components from 'unplugin-vue-components/vite'
import {
  AntDesignVueResolver
} from 'unplugin-vue-components/resolvers'

export default defineConfig({
  //...
  plugins: [
    //...
    Components({
      resolvers: [AntDesignVueResolver()]
    })
  ]
})

```

</div>
</STwoCols>

<!--
Element Plus 是 Element UI 针对 Vue3 的版本，Ant Design Vue 3 以上的版本也都是支持 Vue3 的
 -->

---

# 代码质量管理

ESLint / Husky

---

# 单元测试

Vitest

---

# 其它工具库推荐

<v-clicks>

- 组合函数库 VueUse
- 国际化 vue-i18n
- 图标 unplugin-icons

</v-clicks>

---
layout: center
---

# 谢谢！
