
# API介绍（nuxt,nuxt-child都相当于router-view）

## nuxt 组件
### asyncData
- 该组件只适用于在布局中显示页面组件（即非布局内容）
  layouts/default.vue
``` html
<template>
    <div>
        <div>页头</div>
        <nuxt />
        <div>页脚</div>
    </div>
</template>
```

### nuxt-child组件
- 该组件用于显示嵌套路由场景下的页面内容
``` html
<template>
  <div>
    <h1>我是父级页面</h1>
    <nuxt-child :foobar="123" />
  </div>
</template>
```

### nuxt-link组件（別名: n-link, NuxtLink, 和 NLink）
- nuxt-link 组件用于在页面中添加链接至别的页面
``` html
<template>
  <div>
    <h1>Home page</h1>
    <nuxt-link to="/about">关于</nuxt-link>
  </div>
</template>
```

### client-only组件
- 此组件用于仅在客户端渲染其他组件.
``` html
<template>
  <div>
    <sidebar />
    <client-only placeholder="Loading...">
      <!-- comments 组件只会在客户端被渲染 -->
      <comments />
    </client-only>
  </div>
</template>
```
