
# API介绍

## PAGES
### asyncData
- 在渲染组件之前异步获取数据，并设置组件data数据
``` js
export default {
    data() {
        return { project: 'default' }
    },
    asyncData({ params }, callback) {
        return { project: 'nuxt' }
    }
    asyncData({ params }, callback) {
        axios.get(`https://my-api/posts/${params.id}`).then(res => {
            callback(null, { title: res.data.title })
        })
    }
}
```

### fetch
- 与 asyncData 方法类似，不同的是它不会设置组件的数据
``` js
export default {
    fetch({ store, params }) {
        return axios.get('http://my-api/stars').then(res => {
            store.commit('setStars', res.data)
        })
    }
}
```

### head
- 更新页面的头部标签head和html属性，例如title、meta等等
``` js
head() {
    return {
        title: this.title,
        meta: [
            {
                hid: 'description',
                name: 'description',
                content: 'My custom description'
            }
        ]
    }
}
```

### key
- key属性赋值到<router-view>，这对于在动态页面和不同路径中进行转换很有用。不同的key会使页面组件重新渲染
``` js
key(route) {
    return route.fullPath
}
```

### layout
- 目录下的所有文件都属于个性化布局文件，可以在页面组件中利用 layout 属性来引用
``` js
export default {
    layout: 'blog',
    // 或
    layout(context) {
        return 'blog'
    }
}
```

### loading
- loading 属性为您提供了禁用特定页面上的默认加载进度条的选项。或者可以通过Configuration 的加载选项全局禁用或自定义它
``` js
export default {
    loading: false
}
```

### middleware
- 在应用中的特定页面设置中间件
``` js
export default {
    middleware: 'authenticated'
}
```
- middleware/authenticated.js
``` js
export default function ({ store, redirect }) {
    // If the user is not authenticated
    if (!store.state.authenticated) {
        return redirect('/login')
    }
}
```

### scrollToTop
- scrollToTop 属性用于控制页面渲染前是否滚动至页面顶部
``` js
export default {
    scrollToTop: true
}
```

### transition
- Nuxt.js 使用 Vue.js 的transition组件来实现路由切换时的过渡动效
``` js
export default {
    // 可以是字符
    transition: ''
    // 或对象
    transition: {}
    // 或函数
    transition (to, from) {}
}
export default {
  transition: {
    name: 'test',
    mode: 'out-in'
  }
}
```

### validate
- Nuxt.js 可以让你在动态路由对应的页面组件中配置一个校验方法用于校验动态路由参数的有效性
``` js
validate({ params, query }) {
  return true // 如果参数有效
  return false // 参数无效，Nuxt.js 停止渲染当前页面并显示错误页面
}
async validate({ params, query, store }) {
  // await operations
  return true // 如果参数有效
  return false // 将停止Nuxt.js呈现页面并显示错误页面
}
validate({ params, query, store }) {
  return new Promise((resolve) => setTimeout(() => resolve()))
}
```