# es6Learn
- 1.判断对象是否为null或者undefind 用 obj === null
- 2.通过Object.defineProperty()定义属性,可以添加拦截器Object.defineProperty(obj, 'name', 
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
