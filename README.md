
# 36个JS手写题


### 数据类型判断
```
typeof可以正确识别：Undefined/Boolean/Number/String/Symbol/Function等类型的数据，但是对于其他的都会认为是Object,比如Null/Date等，所以通过typeof来判断数据类型会不准确。但是可以使用Object.protptype.toString实现

function typeOf(obj){
    //评论区里提到的更好的写法
    return Object.prototype.toString.call(obj).slice(8,-1).toLowerCase()
}
typeOf([])    //array
typeOf({})    //object
typeOf(new Date)    //date

```
### 继承
#### 原型链继承
```
function Animal(){
    this.colors = ["black","white"]
}
Animal.prototype.getColor = function(){
  retutn this.colors
}
function Dog(){}

Dog.prototype = new Animal()

let dog1 = new Animal()
dog1.colors.push("brown")
let dog2 = new Dog()
console.log(dog2.colors)    //["black","white","brown"]
```
###### 原型链继承存在的问题
1.原型中包含的引用类型属性将被所有实例共享
2.子类在实例化的时候不能给父类构造函数传参

#### 借用构造函数实现继承
```

function Animal(name){
    this.name = name;
    this.getName = function(){
        return this.name
    }
}

function Dog(name){
  Animal.call(this,name)
}

Dog.prototype = new Animal

```

#### 借用构造函数实现继承解决了原型链继承的问题；引用类型共享问题以及传参问题。但是由于方法必须定义在构造函数中，所以会导致每次创建子类实例都会创建一遍方法。

#### 组合继承
组件继承结合了原型链和盗用构造函数，将两者的优点集中起来.(基本的思路是使用原型链上的属性和方法，而通过盗用构造函数继承实例属性。)

```
function Animal(name){
  this.name = ["black","while"]
}

Animal.prototype.getName = function(){
  return this.name;
}

function Dog(name,age){
  Animal.call(this,name);
  this.age = age
}

Dog.prototype = new Animal()
Dog.prototype.constructor = Dog

let dog1 = new Dog('奶昔',2)
dog1.colors.push('barown')
let dog2 = new Dog('哈赤',1)
console.log(dog2)
//{name:"哈赤",colors:["black","white"],age:1}

```

#### 寄生式组合继承


# vue 脚手架

webpack + vue

## 1. 安装

`https://cli.vuejs.org/zh/guide/`

vue-cli
检测 vue 脚手架版本号
vue -V @vue/cli 4.5.15

## 2. 利用 vue-cli 下载成型的 vue 框架

vue create <name>

```js

Yarn / taobao  Y

1. Manually select features 回车

? Please pick a preset: Manually select features
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert sele
ction)
❯◉ Choose Vue version
 ◉ Babel
 ◯ TypeScript
 ◯ Progressive Web App (PWA) Support
 ◯ Router
 ◯ Vuex
 ◉ CSS Pre-processors
 ◉ Linter / Formatter
 ◯ Unit Testing
 ◯ E2E Testing


2.x 选择 2
3.x

  Sass/SCSS (with dart-sass)
❯ Sass/SCSS (with node-sass)
  Less
  Stylus

 代码格式化规范选择
? Pick a linter / formatter config:

  ESLint with error prevention only
  ESLint + Airbnb config
  ESLint + Standard config
❯ ESLint + Prettier  代码格式化

 ◉ Lint on save   在代码保存的时候，检测代码是否规范
❯◉ Lint and fix on commit  在代码提交到git上的时候，检测代码是否规范

 〉In dedicated config files  挨个保存成单独的文件
   In package.json 保存在这个文件中，

 Save this as a preset for future projects? (y/N) 是否将刚才已经设置过的选项，保存下来，以后接着用

```

## 认识 vue-cli 框架

1. public
2. src
   - main.js 主入口文件
   - App.vue 视图主入口文件
   - assets 静态资源
   - components 组件放置区域（公共组件）
3. package.json

## vue 组件封装原则

子组件：获取/通知
（数据往下流 / 逻辑往上走）

## vue 组件传参

1. 父子传递 （属性传递参数，props 接收）

<TabTile :title="title" v-on:"toParent"="toParent">

1. 子父传参数 (发布 订阅)

this.$emit('toParent', {index:1})


###### 计算属性
计算属性是vue实例中的一个配置选项：computed；
通常里面都是一个个计算相关的函数，函数里头可以写大量的逻辑，最后返回计算出来的值
即我们