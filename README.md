# ES6
- 1.判断对象是否为null或者undefind 用 obj === null
- 2.通过Object.defineProperty()定义属性,可以添加拦截器
```
    Object.defineProperty(obj, 'name', 
      {
        enumerable: true, // 是否可枚举
        configurable: true, // 是否可删除
        get() {
          return str
        },
        set(newStr) {
          str = newStr
        }
      }
    )
```
# Vue 自定义指令
- 1.v-color,通过Vue.directive()定义多是全局指令,directives局部指令
```
    // 全局指令
    Vue.directive('color', (el, bingdings, vnode) => {
      el.style.border = `1px solid ${bingdings.value}`
    })
    // 局部指令
    let vm = new Vue({
        el: '#app',
        directives: {
            'color'(el, bingdings, vnode) {
                el.addEventListener('click', (e) => {
                    if (el.contains(e.target)){ // 是否包含 e.target
                    }
                })
            } 
        }
    })
```
