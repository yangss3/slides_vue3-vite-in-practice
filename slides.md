---
theme: default
title: Vue3 + Vite 前端工程化实践
background: https://picsum.photos/1920/1080
layout: cover
class: text-center
highlighter: shiki
drawings:
  persist: false
---

# Vue3 + Vite 前端工程化实践

从零开始搭建一个基于 Vue3, Vite 和 TypeScript 的前端脚手架

杨书山

<!--
大家晚上好，今天主题是 Vue3 + Vite 的前端工程化实践

然后今天的目标是从零开始搭建一个基于 Vue3，Vite 和 TypeScript 的脚手架
-->

---

# Vue3 & Vite

一个最简单的 Vue3 应用

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
  <script type="module" src="./src/main.js"></script>
</body>
```
</div>
</div>

<!--
vue3 正式版发布已经有一年多了，也是目前最流行的前端框架之一，

从使用者的角度来看，vue3最大的变化应该是更好的typescript支持和Composition API 的引入。
相信大家应该都已经开始用了。这里就不多说了。

然后 Vite 也是最近非常火的一个前端开发和构建工具，它冷启动和热更新速度非常快，web开发工具这一块大有取代webpack之势

我们先从一个最简单应用开始，要在 vite 上把 vue3 的应用跑起来非常简单，大概只需要四部

1. 安装 vue 和 vite

vite 虽然和 vue 出于同一个作者，但是它不是专门为 vue 写的开发工具，它不与任何前端框架绑定。所以我们还需要安装这个官方提供的插件来提供对vue的支持

2. 创建vite配置文件

vite 的一个特点就开箱即用，很多东西有已经预设好了，你基本不需要做多少配置就能用，这里我们只需要注册这个vue插件就行了，这样就提供了对vue的支持

3. 初始化vue应用

  这就是我们写 vue2 应用时的入口文件

  就是创建vue实例，然后挂在到dom节点上

4. 创建应用入口文件

  对于vite项目来说，index.html 才是应用的入口文件，开发环境下，浏览器充当了bundler的角色，浏览器从index.html开始解析你的模块视图

  这里必须要设置 type="module" 这个属性告诉浏览器 src/main.js 是个es 模块，这样它才能正确解析
-->

---

# TypeScript 集成

Vite 提供了开箱即用的 TypeScript 支持

<div class="grid grid-cols-[3fr,2fr] gap-6">
<div>
<div v-click>

**安装 TypeScript**
```bash
npm install -D typescript
```

</div>
<div v-click class="mt-40px">

**从 JS 切换为 TS**

<div class="flex items-center">

<!-- <span class="text-sm mr-3">SFC</span> -->

```html
<script>
export default {
  //...
}
</script>
```

<div class="relative w-50px -top-10px">
 <arrow x1="10" y1="10" x2="40" y2="10" color="gray" width="1" arrowSize="1" />
</div>

```html
<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  //...
})
</script>
```

</div>
<div class="flex items-center">

<div>

`*.js`

</div>
<div class="relative w-50px -top-10px">
 <arrow x1="10" y1="10" x2="40" y2="10" color="gray" width="1" arrowSize="1" />
</div>

<div>

`*.ts`

</div>
<div>
</div>


</div>

</div>
</div>
<div v-click class="relative -top-30px">

**`tsconfig.json`**

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
    "isolatedModules": true,
    "skipLibCheck": true,
    "preserveValueImports": true,
    "importsNotUsedAsValues": true,
    "forceConsistentCasingInFileNames": true,
    "baseUrl": "./",
  }
}
```

</div>
</div>

<!--
vite 提供了开箱即用的 ts 支持

基本上除了安装 typescript之外，不需要做任何其它配置，就可以直接在项目里使用 ts

为了获得更好的类型检查，以及让ts被正确转译，还需要提供一个 tsconfig.json 文件
 -->
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
<!-- <SBadge>推荐</SBadge> -->
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

vite 对这些预处理器都提供了预设，你只需要在项目中安装对应的预处理器，就可以直接使用了

但是我自己现在更倾向于不使用预处理器，less sass 这些毕竟不是标准

其实我们现在可以开始写标准的现代的css，目前的主流的浏览器都在支持，比如 css 变量我们就可以直接用了，至于嵌套语法目前还处于 stage 2 阶段，我们可以通过postcss 插件来支持，这里我推荐一个插件 postcss-preset-env，它的作用类似于 babel，tsc 等等这些转译器，可以帮你把现代的css转换成目前主流浏览器能过理解的语法，所以你可以直接在项目中写现代的 css

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

<!--
这里再推荐一个最近很火的原子css框架，可以让你快速的构建你的 UI，同时你不需要去写很多样式



比如已windicss为例，我们只需要使用它提供的原子类，就能快速实现这样一个 button。

windicss 会按需帮你生成对应的css代码，所以不用担心生成环境的性能问题
-->

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


<!--
vue-router 4 是针对 Vue 3 路由库，它也使用了组合式 API 的写法，在v4里 vue-router 不在是一个类，而是一堆组合函数。
除了这点不一样，其它概念和用法基本和v3 一样，这里就不多说了
 -->

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

<!--

pinia 是 vue 新一代的状态管理库，vuex 因为对TS的支持很差，而且很难在现有的架构下进行改造，所以在vue3里已经不推荐使用了，当然你想用还是可以用

现在官方推荐的状态管理库就是 pinia，基于组合式API，类型友好。它也保留了很多vuex的概念，所以切换起来也很容易

 -->

---

# Script Setup

编译时语法糖，简化 SFC 的代码

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

<!--
比如对这个一个模板，它的script快，我们用正常的写法是这样
-->

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
    Components({
      // default
      dirs: "src/components"
    })
  ]
})
```

</div>
</div>


</STwoCols>


<!--
这个插件默认会将 src/components 里的组件按需导入到你的 sfc 中，并自动帮你注册，

所以你可以在 SFC 的 template里直接使用 src/components 下面定义的组件，不需要手动引入和注册
 -->

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

<!--
很多API在我们在项目中需要经常使用，例如 vue 的那些组合式 api，几乎每个sfc中我们都有用到，所以每次都需要 import 进来会很繁琐，而且它属于体力后。

这个过程可以通过 vite 插件在编译时阶段帮你做
-->

---

# UI 组件库集成

[Element Plus](https://element-plus.gitee.io/zh-CN/) / [Ant Design Vue 3.x](https://www.antdv.com/docs/vue/introduce-cn)

<STwoCols>
<div v-click>

**安装 Element Plus:**
```bash
npm install element-plus
```
```ts
// main.ts
import { createApp } from 'vue'
import App from './App'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'

createApp(App).use(ElementPlus).mount('#app')
```

</div>
<div v-click>

**按需自动导入组件**

```ts
import { defineConfig } from 'vite'
import Components from 'unplugin-vue-components/vite'
import {
  ElementPlusResolver
} from 'unplugin-vue-components/resolvers'

export default defineConfig({
  plugins: [
    Components({
      resolvers: [ElementPlusResolver()]
    })
  ]
})

```

</div>
</STwoCols>

<!--
国内比较早支持vue3的组件库

Element Plus 是 Element UI 针对 Vue3 的版本，Ant Design Vue 3 以上的版本也都是支持 Vue3 的

 -->

---

# 代码质量管理

ESLint / Husky

<STwoCols>

<div>

<v-clicks>

**eslint: 代码风格检查和自动修复**

```bash
npm install -D eslint @yangss/eslint-config-vue
```

```json
// .eslintrc.json
{
  "extends": [
    "@yangss/eslint-config-vue"
  ]
}
```

</v-clicks>

</div>

<div>

<v-clicks>

**husky & lint-staged: 检查并修复当前要提交的代码**

```bash
npm install -D husky lint-staged
npx husky install
npx husky add .husky/pre-commit "npx lint-staged"
```

```json
// package.json
{
  //...
  "lint-staged": {
    "*.(ts|vue)": "eslint --fix"
  }
}
```

</v-clicks>

</div>
</STwoCols>

<!--
代码质量管理在工程化里也是很重要的环节，这里说说怎么通过工具经行代码质量管理

eslint 大家应该都很熟悉，它可以用来检查我们的代码，包括发现一些潜在的 bug，约束代码风格等。
它是可配置的，我们可以定制我们自己代码规范，eslint使用我们提供的规范进行代码检查

这里我自己做了一个规则包 @yangss/eslint-config-vue，里面集成 eslint-plugin-vue，以及包含针对 TS 和 JS 的规则

Husky 是一个帮助你使用 git hook 的工具，利用它你可以非常容易为 git 钩子注册自定义任务，这样就可以让你的工作流自动化，

例如结合lint-staged 可以在每次你提交代码之前自动检查当前提交的代码，通过了检查才能提交成功

 -->
---

# 单元测试

Vitest & test-utils

<v-clicks>

- **[Vitest](https://vitest.dev/)**：基于 Vite 的单元测试框架
- **[Test Utils](https://test-utils.vuejs.org/)**：Vue 官方提供的组件测试工具库

</v-clicks>

---

# 其它工具库推荐

<v-clicks>

- 组合函数库 [VueUse](https://vueuse.org/)
- 国际化插件 [vue-i18n](https://kazupon.github.io/vue-i18n/)
- 图标库 [unplugin-icons](https://github.com/antfu/unplugin-icons)

</v-clicks>

---
layout: center
---

# 谢谢！
