# ES5
- 1.获取可视区域高度方法 document.documentElemnt.clientHeight
- 2.拖拽选框，left 设置是按照哪个值小来设置
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
# Vue
- 1.自定义指令 v-color,通过Vue.directive()定义是全局指令,directives局部指令
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
                document.addEventListener('click', (e) => {
                    if (el.contains(e.target)){ // 是否包含 e.target
                    }
                })
            }
            focus: { // 另外一种指令写法，类似生命周期
                bind(el) {} // 绑定,但还未在页面中出现
                inserted(el) { // 这个元素插入页面中的时候触发
                }
                // 所有的数据发生变化都会执行
                update(el) {} // 依赖的数据发生变化 会触发此方法
            }
        }
    })
```
- 2.vue中过滤器，需要对展示对数据进行包装，但不能改变原来但数据,跟指令一样存在全局和局部,比如 {{xx | toUpper(3)}}, 
|是管道符
```
    // 全局过滤器
    Vue.filter('toUpper', (value, count=1) => {
      return value.slice(0,count).toUpperCase() + value.slice(count)
    })
    
```
- 3.computed 是基于Object.defindProperty实现的计算属性.
- 4.watch和computed的区别,它俩都是计算属性用，但watch可以处理异步,computed处理同步,watch里有三个参数immediate,handler,deep
```
    Vue.$watch({
        firstName: {
            handler() { 
            },
            immediate: true, // 立即执行handler函数
            deep: true // 只要属性发生变化就会触发，默认只触发一次
        }
    })
```
- 5.Vue的生命周期
```
    let vm = new Vue({
        el: '#app',
        beforeCreate () {},// 可以用来挂载自己写的一些方法或者属性
        create () {}, // 响应式的数据变化观察, 无法获取真实的dom
        beforeMount () {}, // 挂载之前，基本上用不到，检测有没有template属性,有template的话就渲染成一个render函数, 如果有就覆盖#app里的内容
        mounted () {} // 可以获得真实的dom
        beforeUpdate() {} // 数据更新前触发
        updated () {} // 数据更新后触发
        beforeDestroy(){} // 销毁前
        destroyed(){} //销毁后
    })
```
- 6.vue根实力的data数据是对象，但自定义函数必须是函数
```
let vm = new Vue({ // 根实例data是对象或者是函数
    data: {
        name: 1111
    }
})
Vue.component('ma-name', { //但子组建data必须是是函数
    data() {
        return {
            name: 111
        }
    }
})
```
- 7.vue插槽
```
      <div id="app">
        <my-name v-slot:default="obj">
           <div>{{obj.v}}{{obj.b}}</div>
        </my-name>
      </div>
    Vue.component('my-name', {
      template: `<div>
          <slot v="123" b="456"></slot>
        </div>`
    })
    let vm = new Vue({
      el: '#app'
    })
```
