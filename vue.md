# vue

## 第一篇：邂逅vue

### 为什么学习Vuejs？

- 我相信每个人学习Vue的目的是各部相同的。

- 可能你的公司正要将原有的项目使用Vue进行重构。

- 也可能是你的公司新项目决定使用Vue的技术栈。

- 当然，如果你现在正在换工作，你会发现招聘前端的需求中，10个有8个都对Vue有或多或少的要求。

- 当然，作为学习者我们知道Vuejs目前非常火，可以说是前端必备的一个技能。

![image-20210916144626455](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916144626455.png)

![image-20210916144639873](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916144639873.png)

![image-20210916144632583](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916144632583.png)

![image-20210916144643999](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916144643999.png)

### 简单的认识一下Vue.js

- Vue (读音 /vjuː/，类似于 **view**)，不要读错。

- Vue是一个渐进式的框架，什么是渐进式的呢？
  - 渐进式意味着你可以将Vue作为你应用的一部分嵌入其中，带来更丰富的交互体验。
  - 或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统。
  - 比如Core+Vue-router+Vuex，也可以满足你各种各样的需求。

- Vue有很多特点和Web开发中常见的高级功能
  - 解耦视图和数据
  - 可复用的组件
  - 前端路由技术
  - 状态管理
  - 虚拟DOM

- 这些特点，你不需要一个个去记住，我们在后面的学习和开发中都会慢慢体会到的，一些技术点我也会在后面进行讲解。

- 学习Vuejs的前提？
  - 从零学习Vue开发，并不需要你具备其他类似于Angular、React，甚至是jQuery的经验。
  - 但是你需要具备一定的HTML、CSS、JavaScript基础。

### Vue.js安装

- 使用一个框架，我们第一步要做什么呢？安装下载它

- 安装Vue的方式有很多：

- 方式一：直接CDN引入
  - 你可以选择引入开发环境版本还是生产环境版本

  ```vue
  <!-- 开发环境版本，包含了有帮助的命令行警告 --> 
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <!-- 生产环境版本，优化了尺寸和速度 -->
  <script src="https://cdn.jsdelivr.net/npm/vue"></script>
  ```

  

- 方式二：下载和引入

```vue
开发环境 https://vuejs.org/js/vue.js
生产环境 https://vuejs.org/js/vue.min.js
```

- 方式三：NPM安装
  - 后续通过webpack和CLI的使用，我们使用该方式。

### Vue的初体验

- 我们来做我们的第一个Vue程序，体验一下Vue的响应式

- **代码做了什么事情？**

- 我们来阅读JavaScript代码，会发现创建了一个Vue对象。

- 创建Vue对象的时候，传入了一些options：{}
  - {}中包含了el属性：该属性决定了这个Vue对象挂载到哪一个元素上，很明显，我们这里是挂载到了id为app的元素上
  - {}中包含了data属性：该属性中通常会存储一些数据
    - 这些数据可以是我们直接定义出来的，比如像上面这样。
    - 也可能是来自网络，从服务器加载的。

- 浏览器执行代码的流程：
  - 执行到10~13行代码显然出对应的HTML
  - 执行第16行代码创建Vue实例，并且对原HTML进行解析和修改。

- 并且，目前我们的代码是可以做到响应式的。

```vue
   <div id="app">
        <p v-if="seen">现在可以看到我了</p>
        <a :href="url">点击我</a>
    </div>
    <script type="text/javascript">
        var app = new Vue({
            el: "#app",
            data: {
                seen: false,
                url: "https://learning.dcloud.io/#/?vid=6"
            }
        });
    </script>
```



### Vue中的MVVM

- 什么是MVVM呢？
  - 通常我们学习一个概念，最好的方式是去看维基百科(对，千万别看成了百度百科)
  - https://zh.wikipedia.org/wiki/MVVM
  - 维基百科的官方解释，我们这里不再赘述。

- 我们直接来看Vue的MVVM

![image-20210916145746550](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916145746550.png)

![image-20210916145757290](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916145757290.png)

### 创建Vue实例传入的options

- 你会发现，我们在创建Vue实例的时候，传入了一个对象options。

- 这个options中可以包含哪些选项呢？
  - 详细解析： [https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E6%95%B0%E6%8D%AE](https://cn.vuejs.org/v2/api/)

- 目前掌握这些选项：
  - **el****:** 
    - 类型：string | HTMLElement
    - 作用：决定之后Vue实例会管理哪一个DOM。
  - **data:** 
    - 类型：Object | Function （组件当中data必须是一个函数）
    - 作用：Vue实例对应的数据对象。
  - **methods:** 
    - 类型：{ [key: string]: Function }
    - 作用：定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用。

### Vue的生命周期

![image-20210916150531791](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916150531791.png)![image-20210916150539819](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916150539819.png)

![image-20210916150623935](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916150623935.png)

## 第二篇：基础语法

### 插值操作

#### 1.Mustache

- 如何将data中的文本数据，插入到HTML中呢？
  - 我们已经学习过了，可以通过Mustache语法(也就是双大括号)。
  - Mustache: 胡子/胡须.

- 我们可以像下面这样来使用，并且数据是响应式的

![image-20210916164025561](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916164025561.png)

#### 2.v-once

- 但是，在某些情况下，我们可能不希望界面随意的跟随改变
  - 这个时候，我们就可以使用一个Vue的指令

- v-once: 
  - 该指令后面不需要跟任何表达式(比如之前的v-for后面是由跟表达式的)

  - 该指令表示元素和组件(组件后面才会学习)只渲染一次，不会随着数据的改变而改变。

代码如下：

```vue
<div id="app">
        <h2>{{message}}</h2>
        <h2 v-once>{{message}}</h2>//只展现一次message的数据，当后面的message发生改变的时候，这个message不会发生改变。
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
            }
        })
    </script>
```

#### 3.v-html

- 某些情况下，我们从服务器请求到的数据本身就是一个HTML代码
  - 如果我们直接通过{{}}来输出，会将HTML代码也一起输出。
  - 但是我们可能希望的是按照HTML格式进行解析，并且显示对应的内容。

- 如果我们希望解析出HTML展示
  - 可以使用v-html指令

    - 该指令后面往往会跟上一个string类型

    - 会将string的html解析出来并且进行渲染

```vue
<div id="app">
        <h2>{{url}}</h2>		//输出：<a href="https://www.bilibili.com/video/BV15741177Eh?p=14&spm_id_from=pageDriver">b站一下<a> 
        <h2 v-html="url"></h2>    //输出：b站一下

    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                url: '<a href="https://www.bilibili.com/video/BV15741177Eh?p=14&spm_id_from=pageDriver">b站一下<a> '
            }
        })
    </script>
```

#### 4.v-text

- v-text作用和Mustache比较相似：都是用于将数据显示在界面中

- v-text通常情况下，接受一个string类型

```vue
 <div id="app">
        <h2>{{message}}</h2>                     //你好啊！！！
        <h2 v-text="message"></h2>               //你好啊！！！
        <!-- message会覆盖掉h2里面的内容 -->
        <!-- 、//如果只有文本的话可以用<v-text></v-text> -->
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
            }
        })
    </script>
```

#### 5.v-pre

- v-pre用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法。

- 比如下面的代码：
  - 第一个h2元素中的内容会被编译解析出来对应的内容
  - 第二个h2元素中会直接显示{{message}}

![image-20210916164841035](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916164841035.png)

#### 6.v-clock

- 在某些情况下，我们浏览器可能会直接显然出未编译的Mustache标签。

- cloak: 斗篷

![image-20210916164955283](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916164955283.png)

### 绑定属性：

#### 1.v-bind介绍和使用

- 前面我们学习的指令主要作用是将值插入到我们模板的内容当中。

- 但是，除了内容需要动态来决定外，某些属性我们也希望动态来绑定。
  - 比如动态绑定a元素的href属性
  - 比如动态绑定img元素的src属性

- 这个时候，我们可以使用v-bind指令：
  - **作用**：动态绑定属性
  - **缩写**：:
  - **预期**：any (with argument) | Object (without argument)
  - **参数**：attrOrProp (optional)

- 下面，我们就具体来学习v-bind的使用。

##### v-bind基础

- v-bind用于绑定一个或多个属性值，或者向另一个组件传递props值(这个学到组件时再介绍)

- 在开发中，有哪些属性需要动态进行绑定呢？
  - 还是有很多的，比如图片的链接src、网站的链接href、动态绑定一些类、样式等等
- v-bind有一个对应的语法糖，也就是简写方式
  - 在开发中，我们通常会使用语法糖的形式，因为这样更加简洁。

- 比如通过Vue实例中的data绑定元素的src和href，代码如下：

```vue
    <div id="app">
        <img v-bind:src="imgURL" alt="">
        <img :src="imgURL" alt="">
        <!-- 两者效果一样 -->
        <!--v-bind的语法糖写法   v-bind---》：   -->
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
                imgURL: "../../images/back-2.jpg"
            }
        })
    </script>
```

##### v-bind绑定class

- 很多时候，我们希望动态的来切换class，比如：
  - 当数据为某个状态时，字体显示红色。
  - 当数据另一个状态时，字体显示黑色。

- 绑定class有两种方式：
  - 对象语法
  - 数组语法

###### 绑定方式：对象语法

- 绑定方式：对象语法
  - 对象语法的含义是:class后面跟的是一个对象。

    

  **对象语法有下面这些用法：**：

```VUE
用法一：直接通过{}绑定一个类
<h2 :class="{'active': isActive}">Hello World</h2>

用法二：也可以通过判断，传入多个值
<h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法三：和普通的类同时存在，并不冲突
注：如果isActive和isLine都为true，那么会有title/active/line三个类
<h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>
```

```vue
案例：
    <div id="app">
        <!-- 固定的class和动态的的class可以共存，不会相互覆盖 -->
        <h2 class="title" :class="{active: isActive,line:isLine}">{{message}}</h2>
        <h2 class="title" :class="getClass()">{{message}}</h2>
        <!-- 调用函数的时候要加小括号，下面的按钮中的那个可以省略 -->
        <button @click="btnClick">切换颜色</button>
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
                isActive: true,
                isLine: true
            },
            methods: {
                btnClick: function() {
                    this.isActive = !this.isActive
                },
                getClass: function() {
                    return {
                        active: this.isActive,
                        line: this.isLine
                            // 要用到本作用域中的变量的时候记住加this.
                    }
                }
            }
        })
    </script>
```



###### 绑定方式：数组语法

- 绑定方式：数组语法
  - 数组语法的含义是:class后面跟的是一个数组。

**数组语法有下面这些用法**：

```vue
用法一：直接通过{}绑定一个类
<h2 :class="['active']">Hello World</h2>

用法二：也可以传入多个值
<h2 :class=“[‘active’, 'line']">Hello World</h2>

用法三：和普通的类同时存在，并不冲突
注：会有title/active/line三个类
<h2 class="title" :class=“[‘active’, 'line']">Hello World</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>
```

##### v-bind绑定style

- 我们可以利用v-bind:style来绑定一些CSS内联样式。

- 在写CSS属性名的时候，比如font-size
  - 我们可以使用驼峰式 (camelCase) fontSize 
  - 或短横线分隔 (kebab-case，记得用单引号括起来) ‘font-size’

- 绑定class有两种方式：
  - 对象语法
  - 数组语法

###### 绑定方式一：对象语法

```vue
:style="{color: currentColor, fontSize: fontSize + 'px'}"
	style后面跟的是一个对象类型
		对象的key是CSS属性名称
		对象的value是具体赋的值，值可以来自于data中的属性

```

```vue
案例：
 <div id="app">
        <!-- 50px必须加上一个单引号，否则当成以后个变量解析的 -->
        <h2 :style="{fontSize: '50px'}">{{message}}</h2>
        <!-- finalsize直接当成一个变量使用了 -->
        <h2 :style="{fontSize: finalsize}">{{message}}</h2>

        <h2 :style="{fontSize: finalsize1+'px',color:finalcolor}">{{message}}</h2>

        <h2 :style="getStyle()">{{message}}</h2>

        <!-- 是方法，记住一定要加（） -->

        <p :style="{'fontSize': finalsize,color:finalcolor}">{{fullName}}</p>
        <!-- 使用computed不需要加（） -->
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
                finalsize: '100px',
                finalsize1: 100,
                finalcolor: 'red',
                firstName: "Lebron",
                lastName: "James"
            },
            // 计算属性
            computed: {
                fullName() {
                    return this.firstName + " " + this.lastName
                }
            },
            //方法
            methods: {
                getStyle() {
                    return {
                        fontSize: this.finalsize1 + 'px',
                        color: this.finalcolor
                    }
                }
            }
        })
    </script>
```



###### 绑定方式二：数组语法

```vue
<div v-bind:style="[baseStyles, overridingStyles]"></div>
	style后面跟的是一个数组类型
		多个值以，分割即可
```

### 计算属性

#### 1.什么是计算属性

- 我们知道，在模板中可以直接通过插值语法显示一些data中的数据。

- 但是在某些情况，我们可能需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示
  - 比如我们有firstName和lastName两个变量，我们需要显示完整的名称。
  - 但是如果多个地方都需要显示完整的名称，我们就需要写多个{{firstName}} {{lastName}}

- 我们可以将上面的代码换成计算属性：

- OK，我们发现计算属性是写在实例的computed选项中的。

- **计算属性中也可以进行一些更加复杂的操作，比如下面的例子**

```vue
  <div id="app">
        <h2>总价格：{{totalPrice}}</h2>

    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                books: [{
                    id: 110,
                    name: '代码大全',
                    prise: 119
                }, {
                    id: 111,
                    name: '代码大全',
                    prise: 112
                }, {
                    id: 112,
                    name: '代码大全',
                    prise: 101
                }, {
                    id: 113,
                    name: '代码大全',
                    prise: 109
                }]
            },
            computed: {
                totalPrice: function() {
                    let result = 0;
                    for (let i = 0; i < this.books.length; i++) {
                        result += this.books[i].prise;
                    }
                    return result;
                }
            }
        })
    </script>
```

#### 2.计算属性的setter和getter

- 每个计算属性都包含一个getter和一个setter
  - 在上面的例子中，我们只是使用getter来读取。
  - 在某些情况下，你也可以提供一个setter方法（不常用）。
  - 在需要写setter的时候，代码如下：

![image-20210916171616662](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916171616662.png)

#### 3.计算属性的缓存

- 我们可能会考虑这样的一个问题：
  - methods和computed看起来都可以实现我们的功能，
  - 那么为什么还要多一个计算属性这个东西呢？
  - 原因：计算属性会进行缓存，如果多次使用时，计算属性只会调用一次。

### 事件监听

- 在前端开发中，我们需要经常和用于交互。
  - 这个时候，我们就必须监听用户发生的时间，比如点击、拖拽、键盘事件等等
  - 在Vue中如何监听事件呢？使用v-on指令

- **v-on****介绍**
  - **作用**：绑定事件监听器
  - **缩写**：@
  - **预期**：Function | Inline Statement | Object
  - **参数**：event

#### 1.v-on基础

- 这里，我们用一个监听按钮的点击事件，来简单看看v-on的使用
  - 下面的代码中，我们使用了v-on:click="counter++”
  - 另外，我们可以将事件指向一个在methods中定义的函数
- 注：v-on也有对应的语法糖：
  - v-on:click可以写成@click

```vue
   <h2>{{counter}}</h2>
        <button v-on:click='increment(10)'>+1</button>
        <button @click='decrement'>-1</button>
```

```vue
 //定义各种各样的方法
            methods: {
                increment(count) {
                    console.log(count);
                    this.counter++;
                },
                decrement() {
                    this.counter--;
                }
            }
```

#### 2.v-on参数

- 当通过methods中定义方法，以供@click调用时，需要**注意参数问题**：

- 情况一：如果该方法不需要额外参数，那么方法后的()可以不添加。
  - 但是注意：如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去

- 情况二：如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件。

![image-20210916173218712](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916173218712.png)

![image-20210916173224651](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916173224651.png)

#### 3.v-on修饰符

- 在某些情况下，我们拿到event的目的可能是进行一些事件处理。

- Vue提供了修饰符来帮助我们方便的处理一些事件：
  - .stop - 调用 event.stopPropagation()。
  - .prevent - 调用 event.preventDefault()。
  - .{keyCode | keyAlias} - 只当事件是从特定键触发时才触发回调。
  - .native - 监听组件根元素的原生事件。
  - .once - 只触发一次回调。

```vue
<!--停止冒泡-- >
<button @click.stop= "doThis">< /button>

<!--阻止默认行为-->
<button @click.prevent="doThis">< /button>
    
<!--阻止默认行为，没有表达式-->
<form @submit.prevent></ form>
    
< !--串联修饰符-->
<button @click.stop.prevent="doThis"></button>
    
<!--键修饰符，键别名-->
<input @keyup.enter="onEnter">
    
<!--键修饰符，键代码-->
<input @keyup.13="onEnter">
    
<!--点击回调只会触发-次-- >
<button @click.once="doThis"></button>
```

### 条件判断

#### 1.v-if、v-else-if、v-else

- 这三个指令与JavaScript的条件语句if、else、else if类似。
- Vue的条件指令可以根据表达式的值在DOM中渲染或销毁元素或组件

- v-if的原理：
  - **v-if后面的条件为false时，对应的元素以及其子元素不会渲染**。
  - 也就是根本没有不会有对应的标签出现在DOM中。

- **案例演示：**

```vue
<div id="app">
        <span v-if="username">
            <label for="one">用户账号：</label>
            <input type="text" id="one" placeholder="填写用户账号" key="one">
        </span>
        <span v-else>
            <label for="two">用户邮箱：</label>
            <input type="text" id="two" placeholder="填写用户邮箱" key="two">
        </span>
        <button @click="username=!username">切换类型</button>
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                username: true
            }
        })
    </script>
```

案例小问题：
- 小问题：
  - 如果我们在有输入内容的情况下，切换了类型，我们会发现文字依然显示之前的输入的内容。
  - 但是按道理讲，我们应该切换到另外一个input元素中了。
  - 在另一个input元素中，我们并没有输入内容。
  - 为什么会出现这个问题呢？

- 问题解答：
  - 这是因为Vue在进行DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。
  - 在上面的案例中，Vue内部会发现原来的input元素不再使用，直接作为else中的input来使用了。

- 解决方案：
  - 如果我们不希望Vue出现类似重复利用的问题，可以给对应的input添加key
  - 并且我们需要保证key的不同

#### 2.v-show

- v-show的用法和v-if非常相似，也用于决定一个元素是否渲染：

- **v-if****和****v-show****对比**

- v-if和v-show都可以决定一个元素是否渲染，那么开发中我们如何选择呢？
  - v-if当条件为false时，压根不会有对应的元素在DOM中。
  - v-show当条件为false时，仅仅是将元素的display属性设置为none而已。

- 开发中如何选择呢？
  - 当需要在显示与隐藏之间切片很频繁时，使用v-show
  - 当只有一次切换时，通过使用v-if

```vue
    <div id="app">
        <h2 v-if="isShow" id="one">{{message}}</h2>
        <h2 v-show="isShow" id="two">{{message}}</h2>
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
                isShow: true
            }
        })
    </script>
```

### 循环遍历

#### 1.v-for遍历数组

- 当我们有一组数据需要进行渲染时，我们就可以使用v-for来完成。
  - v-for的语法类似于JavaScript中的for循环。
  - 格式如下：item in items的形式。

- 我们来看一个简单的案例：

- 如果在遍历的过程中不需要使用索引值
  - v-for="movie in movies"
  - 依次从movies中取出movie，并且在元素的内容中，我们可以使用Mustache语法，来使用movie

- 如果在遍历的过程中，我们需要拿到元素在数组中的索引值呢？
  - 语法格式：v-for=(item, index) in items
  - 其中的index就代表了取出的item在原数组的索引值。

```vue
 <div id="app">
        <ul>
            <li v-for="(item,index) of name">{{index+1}}.{{item}}</li>
        </ul>
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                name: ['fhkjsd', 'adfga', 'sdfasd', 'asdfgsd']
            }
        })
    </script>
```



#### 2.v-for遍历对象

- v-for可以用户遍历对象：
  - 比如某个对象中存储着你的个人信息，我们希望以列表的形式显示出来。

```vue
    遍历对象

    <div id="app">
        <!-- 1.在遍历对象的过程中，如果只是获取一个值，那么获取到的是  value  -->
        <ul>
            <li v-for="item of foo">{{item}}</li>
        </ul>
        <!-- 2.获取key和value 格式：（value,key） -->
        <ul>
            <li v-for="(item,key) of foo">{{key}}:{{item}}</li>
        </ul>
        <!-- 3.获取key,value和索引 格式：（value,key，index） -->
        <ul>
            <li v-for="(item,key,index) of foo">{{index}}-{{key}}:{{item}}</li>
        </ul>
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                foo: {
                    name: 'why', //name:是key,why:是value。
                    age: '21',
                    height: '1.78'
                }
            }
        })
    </script>
```

#### 3.组件的key属性

- **官方推荐我们在使用v-for时，给对应的元素或组件添加上一个:key属性。**

- 为什么需要这个key属性呢（了解）？
  - 这个其实和Vue的虚拟DOM的Diff算法有关系。
  - 这里我们借用[React’s](https://link.zhihu.com/?target=https://calendar.perfplanet.com/2013/diff/)[ diff algorithm](https://link.zhihu.com/?target=https://calendar.perfplanet.com/2013/diff/)中的一张图来简单说明一下：

- 当某一层有很多相同的节点时，也就是列表节点时，我们希望插入一个新的节点
  - 我们希望可以在B和C之间加一个F，Diff算法默认执行起来是这样的。
  - 即把C更新成F，D更新成C，E更新成D，最后再插入E，是不是很没有效率？

- 所以我们需要使用key来给每个节点做一个唯一标识
  - Diff算法就可以正确的识别此节点
  - 找到正确的位置区插入新的节点。

- 所以一句话，**key**的作用主要是为了高效的更新虚拟**DOM**。

![image-20210916203600928](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210916203600928.png)

#### 4.检测数组更新(splice:重点)

- n因为Vue是响应式的，所以当数据发生变化时，Vue会自动检测数据变化，视图会发生对应的更新。
- Vue中包含了一组观察数组编译的方法，使用它们改变数组也会触发视图的更新。
  - push()
  - pop()
  - shift()
  - unshift()
  - splice()
  - sort()
  - reverse()

```vue
  响应式的：
    <div id="app">
        <ul>
            <li v-for="item of letters">{{item}}</li>
        </ul>
        <button @click="btnClick">点击</button>
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                letters: ['a', 'b', 'c', 'd']
            },
            methods: {
                btnClick() {
                    //1.push的方法；在最后面添加元素。
                    // this.letters.push('aaa')
                    //括号中可以跟多个，一次遍历

                    //2.pop();  删除数数组中最后一个元素；
                    // this.letters.pop();

                    //3.shift();    删除数组中的第一个元素；
                    // this.letters.shift();

                    //4.unshift();   在数组的最前面添加元素；
                    // this.letters.unshift('aaaa');
                    //括号中可以跟多个，一次遍历

                    //5.splice();
                    //splice()的作用；删除元素，插入元素，替换元素
                    //splice(start);  从第几个元素开始    第一参数都一样
                    // this.letters.splice(start);

                    //如果是删除元素，第二个参数传入的是你要删除几个元素(如果没有传值就删除后面所有的元素)
                    // this.letters.splice(start,(要删除元素的个数));

                    //替换元素：第二个参数，传入0，并且后面跟上要插入的元素。都好分隔；
                    // this.letters.splice(start,(要替换元素的个数)，（要替换的元素，替换几个写几个）);this.letters.splice(1,3,'b','d','d')

                    //插入元素：
                    // this.letters.splice(1, 0, 'x', 'y', 'z')

                    //6.sort():排序
                    // this.letters.sort()


                    //7.reverse():反转元素；
                    this.letters.reverse()
                    
                    //注意：通过索引直接修改数组中的元素    这不是响应式的
                    // this.letters[0] = 'aaaaa'
                }
            }
        })
    </script>
```

###  v-model

#### 1.表单绑定v-model

- 表单控件在实际开发中是非常常见的。特别是对于用户信息的提交，需要大量的表单。

- Vue中使用v-model指令来实现表单元素和数据的**双向绑定**。

- 案例的解析：
  - 当我们在输入框输入内容时
  - 因为input中的v-model绑定了message，所以会实时将输入的内容传递给message，message发生改变。
  - 当message发生改变时，因为上面我们使用Mustache语法，将message的值插入到DOM中，所以DOM会发生响应的改变。
  - 所以，通过v-model实现了双向的绑定。

- 当然，我们也可以将v-model用于textarea元素

```vue
<div id="app">
        <!-- 双向绑定 -->
        <input type="text" v-model=" message ">
        <!-- 单向绑定   获得data中的message的值 -->
        <input type="text" :value=" message ">
        <!-- 单向绑定    input:获取输入框中的内容事件,输入的值后改变message-->
        <input type="text" v-on:input="valueChange">
        <input type="text" :value=" message " @input="message=$event.target.value">
        <h2>{{message}}</h2>
    </div>
    <script text="javascript ">
        let app = new Vue({
            el: "#app ",
            data: {
                message: "你好啊！！！ ",
            },
            methods: {
                valueChange(event) {
                    this.message = event.target.value;
                }
            }
        })
    </script>
```

#### 2.v-model原理

- v-model其实是一个语法糖，它的背后本质上是包含两个操作：
  - 1.v-bind绑定一个value属性
  - 2.v-on指令给当前元素绑定input事件

- 也就是说下面的代码：等同于下面的代码：

```vue
<input type="text" v-model="message">
等同于
<input type="text" v-bind:value="message" v-on:input="message = $event.target.value">
```

#### 3.v-model:radio和v-model:checkbox

- 当存在多个单选框时

- 复选框分为两种情况：单个勾选框和多个勾选框

- 单个勾选框：
  - v-model即为布尔值。
  - 此时input的value并不影响v-model的值。

- 多个复选框：
  - 当是多个复选框时，因为可以选中多个，所以对应的data中属性是一个数组。
  - 当选中某一个时，就会将input的value添加到数组中。

```vue
案例：
    <div id="app">
        <label for="agree">
            <input type="checkbox" id="agree" v-model="isAgree">喜欢cyl
        </label>

        <h2>你的选择是：{{isAgree}}</h2>
        <button :disabled="!isAgree">下一步</button>
        <br>
        <br> <br>
        <input type="checkbox" value="篮球" v-model="hoddy">篮球
        <input type="checkbox" value="足球" v-model="hoddy">足球
        <input type="checkbox" value="乒乓球" v-model="hoddy">乒乓球
        <input type="checkbox" value="羽毛球" v-model="hoddy">羽毛球
        <h2>你的爱好是：{{hoddy}}</h2>
        <br>
        <br>
        <br>
        <label v-for="item of origilhoddy" :for="item">
            <input type="checkbox" :value="item" :id="item" v-model="hoddy">{{item}}
        </label>
    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
                isAgree: true, //单选框对应的是布尔值
                hoddy: [], //多选框对应的是数组
                origilhoddy: ['篮球', '足球', '乒乓球', '橄榄球', '羽毛球']
            }
        })
    </script>
```

#### 4.v-model:select

- 和checkbox一样，select也分单选和多选两种情况。

- 单选：只能选中一个值。
  - v-model绑定的是一个值。
  - 当我们选中option中的一个时，会将它对应的value赋值到mySelect中

- 多选：可以选中多个值。
  - v-model绑定的是一个数组。
  - 当选中多个值时，就会将选中的option对应的value添加到数组mySelects中

```vue
 <div id="app">
        <!-- 选择一个值 -->
        <select v-model="mySelect">
            <option value="apple">苹果</option>
            <option value="banana">香蕉</option>
            <option value="orange">橘子</option>
        </select>
        <p>你喜欢的水果：{{mySelect}}</p>

        <br>

        <select v-model="mySelects" multiple>
            <option value="apple">苹果</option>
            <option value="banana">香蕉</option>
            <option value="orange">橘子</option>
        </select>
        <p>你喜欢的水果：{{mySelects}}</p>

    </div>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                mySelect: 'apple',
                mySelects: []
            }
        })
    </script>
```

#### 5.值绑定

- 初看Vue官方值绑定的时候，我很疑惑：what the hell is that？

- 但是仔细阅读之后，发现很简单，就是动态的给value赋值而已：
  - 我们前面的value中的值，可以回头去看一下，都是在定义input的时候直接给定的。
  - 但是真实开发中，这些input的值可能是从网络获取或定义在data中的。
  - 所以我们可以通过v-bind:value动态的给value绑定值。
  - 这不就是v-bind吗？

- 这不就是v-bind在input中的应用吗？搞的我看了很久，搞不清他想将什么。

- 这里不再给出对应的代码，因为会用v-bind，就会值绑定的应用了。

#### 6.修饰符

- lazy修饰符：
  - 默认情况下，v-model默认是在input事件中同步输入框的数据的。
  - 也就是说，一旦有数据发生改变对应的data中的数据就会自动发生改变。
  - lazy修饰符可以让数据在失去焦点或者回车时才会更新：

- number修饰符：
  - 默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当做字符串类 型进行处理。
  - 但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理。
  - number修饰符可以让在输入框中输入的内容自动转成数字类型：

- trim修饰符：
  - 如果输入的内容首尾有很多空格，通常我们希望将其去除
  - trim修饰符可以过滤内容左右两边的空格

```vue
   <div id="app">
      <input type="text" v-model.lazy="message">
      <p>当前内容：{{message}}</p>

      年龄：<input type="number" v-model.number="age">
      <p>年龄：{{age}}  类型{{typeof age}}</p>

        <input type="text" v-model.trim="message">
        <p>当前内容：----{{message}}------</p>
    </div>
```

## 第三篇：组件化开发(重点)

### 认识组件化

#### 1.什么是组件化

- 人面对复杂问题的处理方式：
  - 任何一个人处理信息的逻辑能力都是有限的
  - 所以，当面对一个非常复杂的问题时，我们不太可能一次性搞定一大堆的内容。
  - 但是，我们人有一种天生的能力，就是将问题进行拆解。
  - 如果将一个复杂的问题，拆分成很多个可以处理的小问题，再将其放在整体当中，你会发现大的问题也会迎刃而解。

- 组件化也是类似的思想：
  - 如果我们将一个页面中所有的处理逻辑全部放在一起，处理起来就会变得非常复杂，而且不利于后续的管理以及扩展。
  - 但如果，我们讲一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，那么之后整个页面的管理和维护就变得非常容易了。

  

  ![image-20210917093237911](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917093237911.png)

- 我们将一个完整的页面分成很多个组件。

- 每个组件都用于实现页面的一个功能块。

- 而每一个组件又可以进行细分。

#### 2.Vue组件化思想

- 组件化是Vue.js中的重要思想
  - 它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。
  - 任何的应用都会被抽象成一颗组件树。

![image-20210917094218149](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917094218149.png)

- 组件化思想的应用：
  - 有了组件化的思想，我们在之后的开发中就要充分的利用它。
  - 尽可能的将页面拆分成一个个小的、可复用的组件。
  - 这样让我们的代码更加方便组织和管理，并且扩展性也更强。

- 所以，组件是Vue开发中，非常重要的一个篇章，要认真学习。

### 注册组件

#### 注册组件的基本步骤

- 组件的使用分成三个步骤：
  - 创建组件构造器
  - 注册组件
  - 使用组件。

- 我们来看看通过代码如何注册组件

- 查看运行结果：
  - 和直接使用一个div看起来并没有什么区别。
  - 但是我们可以设想，如果很多地方都要显示这样的信息，我们是不是就可以直接使用<my-cpn></my-cpn>来完成呢？  

![image-20210917094715131](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917094715131.png)

#### **注册组件步骤解析**

- 这里的步骤都代表什么含义呢？

- 1.Vue.extend()：
  - 调用Vue.extend()创建的是一个组件构造器。 
  - 通常在创建组件构造器时，传入template代表我们自定义组件的模板。
  - 该模板就是在使用到组件的地方，要显示的HTML代码。
  - 事实上，这种写法在Vue2.x的文档中几乎已经看不到了，它会直接使用下面我们会讲到的语法糖，但是在很多资料还是会提到这种方式，而且这种方式是学习后面方式的基础。

- 2.Vue.component()：
  - 调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称。
  - 所以需要传递两个参数：1、注册组件的标签名 2、组件构造器

- 3.组件必须挂载在某个Vue实例下，否则它不会生效。（见下页）
  - 我们来看下面我使用了三次<my-cpn></my-cpn>
  - 而第三次其实并没有生效：

![image-20210917102718769](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917102718769.png)

#### 组件的其他补充（了解）

##### 1.全局组件和局部组件

- 当我们通过**调用Vue.component()注册组件时，组件的注册是全局的**
  - **这意味着该组件可以在任意Vue示例下使用。**

- 如果我们注册的组件是挂载在某个实例中, 那么就是一个局部组件

![image-20210917103355282](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917103355282.png)

##### 2.父组件和子组件

- 在前面我们看到了组件树：
  - 组件和组件之间存在层级关系
  - 而其中一种非常重要的关系就是父子组件的关系

- 我们来看通过代码如何组成的这种层级关系：

- 父子组件错误用法：以子标签的形式在Vue实例中使用
  - 因为当子组件注册到父组件的components时，Vue会编译好父组件的模块
  - 该模板的内容已经决定了父组件将要渲染的HTML（相当于父组件中已经有了子组件中的内容了）
  - <child-cpn></child-cpn>是只能在父组件中被识别的。
  - 类似这种用法，<child-cpn></child-cpn>是会被浏览器忽略的。

![image-20210917103935024](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917103935024.png)

##### 3.注册组件语法糖

- 在上面注册组件的方式，可能会有些繁琐。
  - Vue为了简化这个过程，提供了注册的语法糖。
  - 主要是省去了调用Vue.extend()的步骤，而是可以直接使用一个对象来代替。

- **语法糖注册全局组件和局部组件**：

![image-20210917104112819](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917104112819.png)

![image-20210917104117500](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917104117500.png)

##### 4.模板的分离写法

- 刚才，我们通过语法糖简化了Vue组件的注册过程，另外还有一个地方的写法比较麻烦，就是template模块写法。

- 如果我们能将其中的HTML分离出来写，然后挂载到对应的组件上，必然结构会变得非常清晰。

- Vue提供了两种方案来定义HTML模块内容：
  - 使用<script>标签
  - 使用<template>标签

![image-20210917104241693](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917104241693.png)

#### 组件的数据存放

##### 1.组件可以访问Vue实例数据吗？

- 组件是一个单独功能模块的封装：
  - 这个模块有属于自己的HTML模板，也应该有属性自己的数据data。

- 组件中的数据是保存在哪里呢？顶层的Vue实例中吗？
  - 我们先来测试一下，组件中能不能直接访问Vue实例中的data

![image-20210917104554840](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917104554840.png)

- 我们发现不能访问，而且即使可以访问，如果将所有的数据都放在Vue实例中，Vue实例就会变的非常臃肿。

- 结论：Vue组件应该有自己保存数据的地方。

##### 2.组件数据的存放

- 组件自己的数据存放在哪里呢?
  - 组件对象也有一个data属性(也可以有methods等属性，下面我们有用到)
  - 只是这个data属性必须是一个函数
  - 而且这个函数返回一个对象，对象内部保存着数据

![image-20210917113741987](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917113741987.png)

- 为什么data在组件中必须是一个函数呢?
  - 首先，如果不是一个函数，Vue直接就会报错。
  - 其次，原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响。

![image-20210917113840850](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917113840850.png)

#### 父子组件的通信

##### 1.引言

- 在上一个小节中，我们提到了子组件是不能引用父组件或者Vue实例的数据的。

- 但是，在开发中，往往一些数据确实需要从上层传递到下层：
  - 比如在一个页面中，我们从服务器请求到了很多的数据。
  - 其中一部分数据，并非是我们整个页面的大组件来展示的，而是需要下面的子组件进行展示。
  - 这个时候，并不会让子组件再次发送一个网络请求，而是直接让**大组件****(****父组件****)**将数据传递给**小组件****(****子组件****)**。

- 如何进行父子组件间的通信呢？Vue官方提到
  -  通过props向子组件传递数据

  - 通过事件向父组件发送消息

![image-20210917114423767](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917114423767.png)

- 在下面的代码中，我直接将Vue实例当做父组件，并且其中包含子组件来简化代码。

- 真实的开发中，**Vue**实例和子组件的通信**和**父组件和子组件的通信过程是一样的。

##### 2.父级向子级传递

###### 2.1props基本用法

- 在组件中，使用选项props来声明需要从父级接收到的数据。

- props的值有两种方式：
  - 方式一：字符串数组，数组中的字符串就是传递时的名称。
  - 方式二：对象，对象可以设置传递时的类型，也可以设置默认值等。

- 我们先来看一个最简单的props传递：

![image-20210917115355453](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917115355453.png)

###### 2.2props数据验证

- 在前面，我们的props选项是使用一个数组。

- 我们说过，除了数组之外，我们也可以使用对象，当需要对**props****进行类型等验证时**，就需要对象写法了。

- 验证都支持哪些数据类型呢？
  - String
  - Number
  - Boolean
  - Array
  - Object
  - Date
  - Function
  - Symbol

- 当我们有自定义构造函数时，验证也支持自定义的类型

![image-20210917115749981](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917115749981.png)

3.子集向父级传递

- props用于父组件向子组件传递数据，还有一种比较常见的是子组件传递数据或事件到父组件中。

- 我们应该如何处理呢？这个时候，我们需要使用**自定义事件**来完成。

- 什么时候需要自定义事件呢？
  - 当子组件需要向父组件传递数据时，就要用到自定义事件了。
  - 我们之前学习的v-on不仅仅可以用于监听DOM事件，也可以用于组件间的自定义事件。

- 自定义事件的流程：
  - 在子组件中，**通过$emit()来触发事件**。
  - 在父组件中，**通过v-on来监听子组件事件**。

- 我们来看一个简单的例子：
  - 我们之前做过一个两个按钮+1和-1，点击后修改counter。
  - 我们整个操作的过程还是在子组件中完成，但是之后的展示交给父组件。
  - 这样，我们就需要将子组件中的counter，传给父组件的某个属性，比如total。

![image-20210917120135564](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917120135564.png)

##### 3.父子组件的访问方式：

###### 3.1$children

- 有时候我们需要父组件直接访问子组件，子组件直接访问父组件，或者是子组件访问跟组件。
  - 父组件访问子组件：使用$children或$refs
  - 子组件访问父组件：使用$parent

- 我们先来看下$children的访问
  - this.$children是一个数组类型，它包含所有子组件对象。
  - 我们这里通过一个遍历，取出所有子组件的message状态。

![image-20210917145920562](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917145920562.png)

###### 3.2**：** **$refs**

- $children的缺陷：
  - 通过$children访问子组件时，是一个数组类型，访问其中的子组件必须通过索引值。
  - 但是当子组件过多，我们需要拿到其中一个时，往往不能确定它的索引值，甚至还可能会发生变化。
  - 有时候，我们想明确获取其中一个特定的组件，这个时候就可以使用$refs

- $refs的使用：
  - $refs和ref指令通常是一起使用的。
  - 首先，我们通过ref给某一个子组件绑定一个特定的ID。
  - 其次，通过this.$refs.ID就可以访问到该组件了。

###### 3.3:**$parent**

- 如果我们想在子组件中直接访问父组件，可以通过$parent

- 注意事项：
  - 尽管在Vue开发中，我们允许通过$parent来访问父组件，但是在真实开发中尽量不要这样做。
  - 子组件应该尽量避免直接访问父组件的数据，因为这样耦合度太高了。
  - 如果我们将子组件放在另外一个组件之内，很可能该父组件没有对应的属性，往往会引起问题。
  - 另外，更不好做的是通过$parent直接修改父组件的状态，那么父组件中的状态将变得飘忽不定，很不利于我的调试和维护。

###### 3.4**非父子组件通信**

- 刚才我们讨论的都是父子组件间的通信，那如果是非父子关系呢?
  - 非父子组件关系包括多个层级的组件，也包括兄弟组件的关系。

- 在Vue1.x的时候，可以通过$dispatch和$broadcast完成
  - $dispatch用于向上级派发事件
  - $broadcast用于向下级广播事件
  - 但是在Vue2.x都被取消了

- 在Vue2.x中，有一种方案是通过**中央事件总线**，也就是一个中介来完成。
  - 但是这种方案和直接使用Vuex的状态管理方案还是逊色很多。
  - 并且Vuex提供了更多好用的功能，所以这里我们暂且不讨论这种方案，后续我们专门学习Vuex的状态管理。

### 插槽

#### 1.**编译作用域**

- 在真正学习插槽之前，我们需要先理解一个概念：编译作用域。

- 官方对于编译的作用域解析比较简单，我们自己来通过一个例子来理解这个概念：

- 我们来考虑下面的代码是否最终是可以渲染出来的：
  - <my-cpn v-show="isShow"></my-cpn>中，我们使用了isShow属性。
  - isShow属性包含在组件中，也包含在Vue实例中。

- 答案：最终可以渲染出来，也就是使用的是Vue实例的属性。

- 为什么呢？
  - 官方给出了一条准则：**父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译。**
  - 而我们在使用<my-cpn v-show="isShow"></my-cpn>的时候，整个组件的使用过程是相当于在父组件中出现的。
  - 那么他的作用域就是父组件，使用的属性也是属于父组件的属性。
  - 因此，isShow使用的是Vue实例中的属性，而不是子组件的属性。

#### 2.为什么使用插槽

- slot翻译为插槽：
  - 在生活中很多地方都有插槽，电脑的USB插槽，插板当中的电源插槽。
  - 插槽的目的是让我们原来的设备具备更多的扩展性。
  - 比如电脑的USB我们可以插入U盘、硬盘、手机、音响、键盘、鼠标等等。

- 组件的插槽：
  - 组件的插槽也是为了让我们封装的组件更加具有扩展性。
  - 让使用者可以决定组件内部的一些内容到底展示什么。

- 例子：移动网站中的导航栏。
  - 移动开发中，几乎每个页面都有导航栏。
  - 导航栏我们必然会封装成一个插件，比如nav-bar组件。
  - 一旦有了这个组件，我们就可以在多个页面中复用了。

- 但是，每个页面的导航是一样的吗？No，我以京东M站为例

#### 3.**如何封装这类组件呢？**slot

- 如何去封装这类的组件呢？
  - 它们也很多区别，但是也有很多共性。
  - 如果，我们每一个单独去封装一个组件，显然不合适：比如每个页面都返回，这部分内容我们就要重复去封装。
  - 但是，如果我们封装成一个，好像也不合理：有些左侧是菜单，有些是返回，有些中间是搜索，有些是文字，等等。

- 如何封装合适呢？抽取共性，保留不同。
  - 最好的封装方式就是将共性抽取到组件中，将不同暴露为插槽。
  - 一旦我们预留了插槽，就可以让使用者根据自己的需求，决定插槽中插入什么内容。
  - 是搜索框，还是文字，还是菜单。由调用者自己来决定。

- 这就是为什么我们要学习组件中的插槽slot的原因。

#### 4.slot基本使用

- 了解了为什么用slot，我们再来谈谈如何使用slot？
  - 在子组件中，使用特殊的元素<slot>就可以为子组件开启一个插槽。
  - 该插槽插入什么内容取决于父组件如何使用。

- 我们通过一个简单的例子，来给子组件定义一个插槽：
  - <slot>中的内容表示，如果没有在该组件中插入任何其他内容，就默认显示该内容
  - 有了这个插槽后，父组件如何使用呢？

![image-20210917153631921](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917153631921.png)

#### 5.具名插槽slot

- 当子组件的功能复杂时，子组件的插槽可能并非是一个。
  - 比如我们封装一个导航栏的子组件，可能就需要三个插槽，分别代表左边、中间、右边。
  - 那么，外面在给插槽插入内容时，如何区分插入的是哪一个呢？
  - 这个时候，我们就需要给插槽起一个名字

- 如何使用具名插槽呢？
  - 非常简单，只要给slot元素一个name属性即可
  - <slot name='myslot'></slot>

- 我们来给出一个案例：
  - 这里我们先不对导航组件做非常复杂的封装，先了解具名插槽的用法。

```vue
 <div id="app">
        <cpn><button slot="middle">按钮</button></cpn>
        <cpn><span slot="left">哈哈哈哈</span></cpn>
    </div>
    <template id="cpn">
        <div>
            <slot name="left"><span>左边</span></slot>
            <slot name="middle"><span>中间的</span></slot>
            <slot name="right"><span>右边</span></slot>
            <slot><button>按钮替换</button></slot>
        </div>
    </template>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
            },
            components: {
                cpn: {
                    template: '#cpn'
                }
            }
        })
    </script>
```

#### 6.作用域插槽

- 作用域插槽是slot一个比较难理解的点，而且官方文档说的又有点不清晰。

- 这里，我们用一句话对其做一个总结，然后我们在后续的案例中来体会：
  - 父组件替换插槽的标签，但是内容由子组件来提供。

- 我们先提一个需求：
  - 子组件中包括一组数据，比如：pLanguages: ['JavaScript', 'Python', 'Swift', 'Go', 'C++']
  - 需要在多个界面进行展示：
    - 某些界面是以水平方向一一展示的，
    - 某些界面是以列表形式展示的，
    - 某些界面直接展示一个数组
  - 内容在子组件，希望父组件告诉我们如何展示，怎么办呢？
    - 利用slot作用域插槽就可以了

- 我们来看看子组件的定义：

- 在父组件使用我们的子组件时，从子组件中拿到数据：

  - 我们通过<template slot-scope="slotone">获取到slotone属性

  - 在通过slotone.data就可以获取到刚才我们传入的data了

```VUE
 <div id="app">
        <cpn></cpn>
        <cpn>
            <template slot-scope="slotone">
                <div>
                    <span v-for="item of slotone.data">{{item}}- </span>
                </div>
            </template>
        </cpn>
    </div>
    <template id="cpn">
        <div>
            <!-- data:这是自己起的名字 -->
            <slot :data="pLanguages">
            <ul>
                <li v-for="item of pLanguages">{{item}}</li>
            </ul>
            </slot>
        </div>
    </template>
    <script text="javascript">
        let app = new Vue({
            el: "#app",
            data: {
                message: "你好啊！！！",
            },
            components: {
                cpn: {
                    template: '#cpn',
                    data() {
                        return {
                            pLanguages: ['大熊', '熊大', '熊二', '光头强']
                        }
                    }
                }
            }
        })
    </script>
```

## 第四篇：Vue Cli相关

### 1.什么是Vue Cli

- 如果你只是简单写几个Vue的Demo程序, 那么你不需要Vue CLI.

- 如果你在开发大型项目, 那么你需要, 并且必然需要使用Vue CLI
  - 使用Vue.js开发大型应用时，我们需要考虑代码目录结构、项目结构和部署、热加载、代码单元测试等事情。
  - 如果每个项目都要手动完成这些工作，那无以效率比较低效，所以通常我们会使用一些脚手架工具来帮助完成这些事情。

- **CLI是什么意思?**
  - CLI是Command-Line Interface, 翻译为命令行界面, 但是俗称脚手架.
  - Vue CLI是一个官方发布 vue.js 项目脚手架
  - 使用 vue-cli 可以快速搭建Vue开发环境以及对应的webpack配置.

### 2.Vue Cli使用的前提 - Node

- **安装NodeJS**
  - 可以直接在官方网站中下载安装.
  - 网址: http://nodejs.cn/download/

- **检测安装的版本**
  -  默认情况下自动安装Node和NPM
  - Node环境要求8.9以上或者更高版本

- **什么是****NPM****呢****?**
  - NPM的全称是Node Package Manager
  - 是一个NodeJS包管理和分发工具，已经成为了非官方的发布Node模块（包）的标准。
  - 后续我们会经常使用NPM来安装一些开发过程中依赖包.

**注：cnpm安装**

- 由于国内直接使用 npm 的官方镜像是非常慢的，这里推荐使用淘宝 NPM 镜像。

- 你可以使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:npm install -g cnpm --registry=https://registry.npm.taobao.org

  这样就可以使用 cnpm 命令来安装模块了：cnpm install [name]

注：具体的安装可以分为命令行安装和图像化界面安装，看哪个适合，这一部分初学者最好是自己先摸索如何安装和使用，如果自己没有配置或者安装好，找已经走过本阶段的学长学姐或则朋友指导如何安装。

流程：

- 安装node.js
- 更改node.js在电脑中的位置
- 配置环境
- （cnpm安装）
- 安装脚手架
- 安装一系列的依赖（npm install xxxx）
- 写作品

## 第五篇：vue-router详解

### 认识路由

#### 什么是路由？

- 说起路由你想起了什么？
  - 路由是一个网络工程里面的术语。
  - **路由**（**routing**）就是通过互联的网络把信息从源地址传输到目的地址的活动. --- 维基百科

- 额, 啥玩意? 没听懂
  - 在生活中, 我们有没有听说过路由的概念呢? 当然了, 路由器嘛.
  - 路由器是做什么的? 你有想过吗?
  - 路由器提供了两种机制: 路由和转送.
    -  路由是决定数据包从**来源**到**目的地**的路径.
    - 转送将**输入端**的数据转移到合适的**输出端**.

- 路由中有一个非常重要的概念叫路由表.
  - 路由表本质上就是一个映射表, 决定了数据包的指向.

#### 后端路由阶段

- 早期的网站开发整个HTML页面是由服务器来渲染的.
  - 服务器直接生产渲染好对应的HTML页面, 返回给客户端进行展示.

- 但是, 一个网站, 这么多页面服务器如何处理呢?
  - 一个页面有自己对应的网址, 也就是URL.
  - URL会发送到服务器, 服务器会通过正则对该URL进行匹配, 并且最后交给一个Controller进行处理.
  - Controller进行各种处理, 最终生成HTML或者数据, 返回给前端.
  - 这就完成了一个IO操作.

- 上面的这种操作, 就是后端路由.
  - 当我们页面中需要请求不同的**路径**内容时, 交给服务器来进行处理, 服务器渲染好整个页面, 并且将页面返回给客户顿.
  - 这种情况下渲染好的页面, 不需要单独加载任何的js和css, 可以直接交给浏览器展示, 这样也有利于SEO的优化.

- 后端路由的缺点:
  - 一种情况是整个页面的模块由后端人员来编写和维护的.
  - 另一种情况是前端开发人员如果要开发页面, 需要通过PHP和Java等语言来编写页面代码.
  - 而且通常情况下HTML代码和数据以及对应的逻辑会混在一起, 编写和维护都是非常糟糕的事情.

#### 前端路由阶段

- 前后端分离阶段：
  - 随着Ajax的出现, 有了前后端分离的开发模式.
  - 后端只提供API来返回数据, 前端通过Ajax获取数据, 并且可以通过JavaScript将数据渲染到页面中.
  - 这样做最大的优点就是前后端责任的清晰, 后端专注于数据上, 前端专注于交互和可视化上.
  - 并且当移动端(iOS/Android)出现后, 后端不需要进行任何处理, 依然使用之前的一套API即可.
  - 目前很多的网站依然采用这种模式开发.

- **单页面富应用阶段**:
  - 其实SPA最主要的特点就是在前后端分离的基础上加了一层前端路由.
  - 也就是前端来维护一套路由规则.

- 前端路由的核心是什么呢？
  - 改变URL，但是页面不进行整体的刷新。
  - 如何实现呢？

### 前端路由的规则

#### 1.URL的hash

- URL的hash
  - URL的hash也就是锚点(#), 本质上是改变window.location的href属性.
  - 我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新

![image-20210917173942128](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917173942128.png)

#### 2.HTML5的history模式：**pushState**

- history接口是HTML5新增的, 它有五种模式改变URL而不刷新页面.

- history.pushState()

![image-20210917174020411](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917174020411.png)

#### 3.HTML5的history模式：r**eplaceState**

- history.replaceState()

![image-20210917174053141](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917174053141.png)

#### 4.HTML5的history模式：go

- history.go()

![image-20210917174145081](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917174145081.png)

- **补充说明：**
  - 上面只演示了三个方法
  - 因为 history.back() 等价于 history.go(-1)
  - history.forward() 则等价于 history.go(1)
  - 这三个接口等同于浏览器界面的前进后退

### vue-router基础

#### 1.认识vue-router

- 目前前端流行的三大框架, 都有自己的路由实现:
  - Angular的ngRouter
  - React的ReactRouter
  - Vue的vue-router

- 当然, 我们的重点是vue-router
  - vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。
  - 我们可以访问其官方网站对其进行学习: https://router.vuejs.org/zh/

- vue-router是基于路由和组件的
  - 路由用于设定访问路径, 将路径和组件映射起来.
  - 在vue-router的单页面应用中, 页面的路径的改变就是组件的切换.

#### 2.**安装和使用**vue-router

- 后续开发中我们主要是通过工程化的方式进行开发的.
  - 所以在后续, 我们直接使用npm来安装路由即可.

  - 步骤一: 安装vue-router

    - npm install vue-router --save

  - 步骤二: 在模块化工程中使用它(因为是一个插件, 所以可以通过Vue.use()来安装路由功能)

    - 第一步：导入路由对象，并且调用 Vue.use(VueRouter)

    - 第二步：创建路由实例，并且传入路由映射配置

    - 第三步：在Vue实例中挂载创建的路由实例

      import Vue from 'vue' 

      import VueRouter from 'vue-route

      Vue.use(VueRouter)

- 使用vue-router的步骤:
  - 第一步: 创建路由组件
  - 第二步: 配置路由映射: 组件和路径映射关系
  - 第三步: 使用路由: 通过<router-link>和<router-view>

##### 2.1创建router实例

![image-20210917214946041](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917214946041.png)

##### 2.2挂在到Vue实例中

![image-20210917215206335](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917215206335.png)

##### 2.3创建路由组件

![image-20210917215258160](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917215258160.png)

##### 2.4配置组件和路径的映射关系

![image-20210917215342996](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917215342996.png)

##### 2.5使用路由

![image-20210917215452324](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917215452324.png)

- <router-link>: 该标签是一个vue-router中已经内置的组件, 它会被渲染成一个<a>标签.（跳转路由）

- <router-view>: 该标签会根据当前的路径, 动态渲染出不同的组件.

- 网页的其他内容, 比如顶部的标题/导航, 或者底部的一些版权信息等会和<router-view>处于同一个等级.

- **在路由切换时, 切换的是<router-view>挂载的组件, 其他内容不会发生改变.**

##### 2.6最终的效果如下：

![image-20210917215809296](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917215809296.png)

#### 3.路由的补充说明：

##### 3.1路由的默认路径

- 我们这里还有一个不太好的实现:
  - 默认情况下, 进入网站的首页, 我们希望<router-view>渲染首页的内容.
  - 但是我们的实现中, 默认没有显示首页组件, 必须让用户点击才可以.

- 如何可以让**路径**默认跳到到**首页**, 并且<router-view>渲染首页组件呢?
  - 非常简单, 我们只需要配置多配置一个映射就可以了.

![image-20210917220011612](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917220011612.png)

- 配置解析:
  - 我们在routes中又配置了一个映射. 
  - path配置的是根路径: /
  - redirect是重定向, 也就是我们将根路径重定向到/home的路径下, 这样就可以得到我们想要的结果了.

##### 3.2HTML的History模式

- 我们前面说过改变路径的方式有两种:
  - URL的hash
  - HTML5的history
  - 默认情况下, 路径的改变使用的URL的hash.

- 如果希望使用HTML5的history模式, 非常简单, 进行如下配置即可:

![image-20210917220157839](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917220157839.png)

**效果如下图：**

![image-20210917220226164](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917220226164.png)

##### 3.3router-link补充

- 在前面的<router-link>中, 我们只是使用了一个属性: to, **用于指定跳转的路径.**

- <router-link>还有一些**其他属性**:
  - tag: tag可以指定<router-link>之后渲染成什么组件, 比如上面的代码会被渲染成一个<li>元素, 而不是<a>
  - replace: replace不会留下history记录, 所以指定replace的情况下, 后退键返回不能返回到上一个页面中
  - **（多了解）**active-class: 当<router-link>对应的路由匹配成功时, 会自动给当前元素设置一个router-link-active的class, 设置active-class可以修改默认的名称.
    - 在进行高亮显示的导航菜单或者底部tabbar时, 会使用到该类.
    - 是通常不会修改类的属性, 会直接使用默认的router-link-active即可. 

![image-20210917220647635](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917220647635.png)

##### 3.4修改linkActiveClass

- 该class具体的名称也可以通过router实例的属性进行修改 

- nexact-active-class

  - 类似于active-class, 只是在精准匹配下才会出现的class.

  - 后面看到嵌套路由时, 我们再看下这个属性.

![image-20210917221114308](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917221114308.png)

![image-20210917221122534](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917221122534.png)

##### 3.5**路由代码跳转**

- 有时候, 页面的跳转可能需要执行对应的JavaScript代码, 这个时候, 就可以使用第二种跳转方式了

- 比如, 我们将代码修改如下: 

![image-20210917221239275](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917221239275.png)

##### 3.6动态路由

- 在某些情况下，一个页面的path路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：
  - /user/aaaa或/user/bbbb
  - 除了有前面的/user之外，后面还跟上了用户的ID
  - 这种path和Component的匹配关系，我们称之为动态路由(也是路由传递数据的一种方式)。

![image-20210917222223281](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917222223281.png)

![image-20210917222229966](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917222229966.png)

![image-20210917222234793](C:/Users/16337/AppData/Roaming/Typora/typora-user-images/image-20210917222234793.png)

![image-20210917222240299](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917222240299.png)

#### 4.路由懒加载

##### 4.1认识路由的懒加载

- 官方给出了解释:
  - 当打包构建应用时，Javascript 包会变得非常大，影响页面加载。
  - 如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了

- 官方在说什么呢?
  - 首先, 我们知道路由中通常会定义很多不同的页面.
  - 这个页面最后被打包在哪里呢? 一般情况下, 是放在一个js文件中.
  - 但是, 页面这么多放在一个js文件中, 必然会造成这个页面非常的大.
  - 如果我们一次性从服务器请求下来这个页面, 可能需要花费一定的时间, 甚至用户的电脑上还出现了短暂空白的情况.
  - 如何避免这种情况呢? 使用路由懒加载就可以了.

- 路由懒加载做了什么?
  - 路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块.
  - 只有在这个路由被访问到的时候, 才加载对应的组件

##### 4.2路由懒加载的效果

![image-20210917222642624](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917222642624.png)

##### 4.3**懒加载的方式**

- 方式一: 结合Vue的异步组件和Webpack的代码分析.

```vue
const Home = resolve => { require.ensure(['../components/Home.vue'], () => { resolve(require('../components/Home.vue')) })};=
```

- 方式二: AMD写法

```vue
const About = resolve => require(['../components/About.vue'], resolve);
```

- 方式三: 在ES6中, 我们可以有更加简单的写法来组织Vue异步组件和Webpack的代码分割.

```vue
const Home = () => import('../components/Home.vue')
```

#### 5.嵌套路由

##### 5.1认识嵌套路由

- 嵌套路由是一个很常见的功能
  - 比如在home页面中, 我们希望通过/home/news和/home/message访问一些内容.
  - 一个路径映射一个组件, 访问这两个路径也会分别渲染两个组件.

- 路径和组件的关系如下:

![image-20210917223040047](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917223040047.png)

- 实现嵌套路由有两个步骤:
  - 创建对应的子组件, 并且在路由映射中配置对应的子路由.
  - 在组件内部使用<router-view>标签.

##### 5.2嵌套路由的实现

1.定义两个组件

![image-20210917223544273](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917223544273.png)

2.router中路由嵌套

![image-20210917223549911](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917223549911.png)

3.实际页面中跳转路由

![image-20210917223555290](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917223555290.png)

4.效果图；

![image-20210917223603567](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917223603567.png)

##### 5.3嵌套默认路径

- 嵌套路由也可以配置默认的路径, 配置方式如下: 

![image-20210917223806837](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210917223806837.png)

#### 6.传递参数

##### 6.1准备工作

- 为了演示传递参数, 我们这里再创建一个组件, 并且将其配置好
  - 第一步: 创建新的组件Profile.vue ![image-20210918091057560](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918091057560.png)

  - 第二步: 配置路由映射 ![image-20210918091114937](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918091114937.png)

  - 第三步: 添加跳转的<router-link>![image-20210918091120935](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918091120935.png)

##### 6.2**传递参数的方式**

- **params的类型:**
  - 配置路由格式: /router/:id
  - 传递的方式: 在path后面跟上对应的值
  - 传递后形成的路径: /router/123, /router/abc

- **query的类型:**
  - 配置路由格式: /router, 也就是普通配置
  - 传递的方式: 对象中使用query的key作为传递方式
  - 传递后形成的路径: /router?id=123, /router?id=abc

- 如何使用它们呢? 也有两种方式: <router-link>的方式和JavaScript代码方式

###### 6.2.1**传递参数方式一: <router-link>**

![image-20210918091704575](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918091704575.png)

###### 6.2.2**传递参数方式二: JavaScript代码**

![image-20210918091740405](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918091740405.png)

##### 6.3获取路由参数

- 获取参数通过$route对象获取的.
  - 在使用了 vue-router 的应用中，路由对象会被注入每个组件中，赋值为 this.$route ，并且当路由切换时，路由对象会被更新。

- 通过$route获取传递的信息如下:

![image-20210918091845488](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918091845488.png)

##### 6.4$route和$router是什么区别的

- $route和$router是有区别的
  - $router为VueRouter实例，想要导航到不同URL，则使用$router.push方法
  - $route为**当前router**跳转对象里面可以获取name、path、query、params等 

![image-20210918092100296](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918092100296.png)

#### 7.导航守卫

##### 7.1为什么使用导航守卫

- 我们来考虑一个需求: 在一个SPA应用中, 如何改变网页的标题呢?
  - 网页标题是通过<title>来显示的, 但是SPA只有一个固定的HTML, 切换不同的页面时, 标题并不会改变.
  - 但是我们可以通过JavaScript来修改<title>的内容.window.document.title = '新的标题'.
  - 那么在Vue项目中, 在哪里修改? 什么时候修改比较合适呢?

- 普通的修改方式:
  - 我们比较容易想到的修改标题的位置是每一个路由对应的组件.vue文件中.
  - 通过mounted声明周期函数, 执行对应的代码进行修改即可.
  - 但是当页面比较多时, 这种方式不容易维护(因为需要在多个页面执行类似的代码).

- 有没有更好的办法呢? 使用导航守卫即可.

- 什么是导航守卫?（重点）
  - vue-router提供的导航守卫主要用来监听路由的进入和离开的.
  - vue-router提供了beforeEach和afterEach的钩子函数, 它们会在路由即将改变前和改变后触发.

##### 7.2导航守卫使用

- 我们可以利用beforeEach来完成标题的修改.
  - 首先, 我们可以在钩子当中定义一些标题, 可以利用meta来定义
  - 其次, 利用导航守卫,修改我们的标题.

- 导航钩子的三个参数解析:
  - to: 即将要进入的目标的路由对象.
  - from: 当前导航即将要离开的路由对象.
  - **next: 调用该方法后, 才能进入下一个钩子**.![image-20210918092824949](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918092824949.png)![image-20210918092830143](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918092830143.png)

##### 7.3导航守卫的补充

- 补充一:**如果是后置钩子, 也就是afterEach, 不需要主动调用next()函数.**

- 补充二: 上面我们使用的导航守卫, 被称之为**全局守卫**.
  - 路由独享的守卫.
  - 组件内的守卫.

- 更多内容, 可以查看官网进行学习:
  - [https://router.vuejs.org/zh/guide/advanced/navigation-guards.html#%E8%B7%AF%E7%94%B1%E7%8B%AC%E4%BA%AB%E7%9A%84%E5%AE%88%E5%8D%AB](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)

#### 8.keep-alive遇见vue-router（重点）

- keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。
  - 它们有两个非常重要的属性:
  - include - 字符串或正则表达，只有匹配的组件会被缓存
  - exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存

- router-view 也是一个组件，如果直接被包在 keep-alive 里面，所有路径匹配到的视图组件都会被缓存：

![image-20210918093059724](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918093059724.png)

- 通过create声明周期函数来验证

## 第六篇：Vuex详解

### 1.认识Vuex

#### 1.1Vuex是做什么的？

- 官方解释：Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。
  - 它采用 集中式存储管理 应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
  - Vuex 也集成到 Vue 的官方调试工具 [devtools](https://github.com/vuejs/vue-devtools)[ extension](https://github.com/vuejs/vue-devtools)，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

- **状态管理**到底是什么？
  - **状态管理模式、集中式存储管理**这些名词听起来就非常高大上，让人捉摸不透。
  - 其实，你可以简单的将其看成把需要多个组件共享的变量全部存储在一个对象里面。
  - 然后，将这个对象放在顶层的Vue实例中，让其他组件可以使用。
  - 那么，多个组件是不是就可以共享这个对象中的所有变量属性了呢？

- 等等，如果是这样的话，为什么官方还要专门出一个插件Vuex呢？难道我们不能自己封装一个对象来管理吗？
  - 当然可以，只是我们要先想想VueJS带给我们最大的便利是什么呢？没错，就是响应式。
  - 如果你自己封装实现一个对象能不能保证它里面所有的属性做到响应式呢？当然也可以，只是自己封装可能稍微麻烦一些。
  - 不用怀疑，Vuex就是为了提供这样一个在多个组件间共享状态的插件，用它就可以了。

#### 1.2管理什么状态呢？

- 但是，有什么状态时需要我们在多个组件间共享的呢？
  - 如果你做过大型开放，你一定遇到过多个状态，在多个界面间的共享问题。
  - 比如用户的登录状态、用户名称、头像、地理位置信息等等。
  - 比如商品的收藏、购物车中的物品等等。
  - 这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的（待会儿我们就可以看到代码了，莫着急）。

- OK，从理论上理解了状态管理之后，让我们从实际的代码再来看看状态管理。
  - 毕竟，Talk is cheap, Show me the code.(来自Linus)

- 我们先来看看单界面的状态管理吧.

#### 1.3单界面的状态管理

- 我们知道，要在单个组件中进行状态管理是一件非常简单的事情
  - 什么意思呢？我们来看下面的图片。

- 这图片中的三种东西，怎么理解呢？
  - State：不用多说，就是我们的状态。（你姑且可以当做就是data中的属性）
  - View：视图层，可以针对State的变化，显示不同的信息。（这个好理解吧？）
  - Actions：这里的Actions主要是用户的各种操作：点击、输入等等，会导致状态的改变。

![image-20210918104703193](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918104703193.png)

#### 1.4单页面状态管理的实现

![image-20210918105554285](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918105554285.png)

- 在这个案例中，我们有木有状态需要管理呢？没错，就是个数counter。

- counter需要某种方式被记录下来，也就是我们的State。

- counter目前的值需要被显示在界面中，也就是我们的View部分。

- 界面发生某些操作时（我们这里是用户的点击，也可以是用户的input），需要去更新状态，也就是我们的Actions

- 这不就是上面1.3的流程图了吗？

#### 1.5多页面状态管理

- **Vue已经帮我们做好了单个界面的状态管理，但是如果是多个界面呢？**
  - 多个视图都依赖同一个状态（一个状态改了，多个界面需要进行更新）
  - 不同界面的Actions都想修改同一个状态（Home.vue需要修改，Profile.vue也需要修改这个状态）

- 也就是说对于某些状态(状态1/状态2/状态3)来说只属于我们某一个试图，但是也有一些状态(状态a/状态b/状态c)属于多个试图共同想要维护的
  - 状态1/状态2/状态3你放在自己的房间中，你自己管理自己用，没问题。
  - 但是状态a/状态b/状态c我们希望交给一个大管家来统一帮助我们管理！！！
  - 没错，Vuex就是为我们提供这个大管家的工具。

- 全局单例模式（大管家）
  - 我们现在要做的就是将共享的状态抽取出来，交给我们的大管家，统一进行管理。
  - 之后，你们每个试图，按照我**规定好的**规定，进行访问和修改等操作。
  - 这就是Vuex背后的基本思想。

#### 1.6Vuex状态管理图例

- 一起在来看一幅官方给出的图片![image-20210918110308429](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918110308429.png)

### 2.Vuex的基本使用

#### 2.1通过案例来了解Vuex的使用

- 我们还是简单的实现一个计数器的案例

- 首先，我们需要在某个地方存放我们的Vuex代码：
  - 这里，我们先创建一个文件夹store，并且在其中创建一个index.js文件
  - 在index.js文件中写入如下代码：

![image-20210918110736448](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918110736448.png)

#### 2.2挂载到Vue实例中

- 其次，我们让所有的Vue组件都可以使用这个store对象
  - 来到main.js文件，导入store对象，并且放在new Vue中
  - 这样，在其他Vue组件中，我们就可以通过this.$store的方式，获取到这个store对象了

![image-20210918110916538](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918110916538.png)

#### 2.3使用Vuex的count

![image-20210918111003098](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918111003098.png)

- 好的，这就是使用Vuex最简单的方式了。

- 我们来对使用步骤，做一个简单的小节：
  - 1.提取出一个公共的store对象，用于保存在多个组件中共享的状态
  - 2.将store对象放置在new Vue对象中，这样可以保证在所有的组件中都可以使用到
  - 3.在其他组件中使用store对象中保存的状态即可
    - 通过this.$store.state.属性的方式来访问状态
    - 通过this.$store.commit('mutation中方法')来修改状态
    - mutation中的方法是对state中定义的变量或则其他东西进行修改。（重点）

- 注意事项：
  - 我们通过提交mutation的方式，而非直接改变store.state.count。
  - 这是因为Vuex可以更明确的追踪状态的变化，所以不要直接改变store.state.count的值。

### 3.Vuex核心概念

- Vuex有几个比较核心的概念:
  - State
  - Getters
  - Mutation
  - Action
  - Module

- 我们对它进行一一介绍.

#### 3.1  State

##### 3.1.1 State单一状态树

- Vuex提出使用单一状态树, 什么是单一状态树呢？
  - 英文名称是Single Source of Truth，也可以翻译成单一数据源。

- 但是，它是什么呢？我们来看一个生活中的例子。
  - OK，我用一个生活中的例子做一个简单的类比。
  - 我们知道，在国内我们有很多的信息需要被记录，比如上学时的个人档案，工作后的社保记录，公积金记录，结婚后的婚姻信息，以及其他相关的户口、医疗、文凭、房产记录等等（还有很多信息）。
  - 这些信息被分散在很多地方进行管理，有一天你需要办某个业务时(比如入户某个城市)，你会发现你需要到各个对应的工作地点去打印、盖章各种资料信息，最后到一个地方提交证明你的信息无误。
  - 这种保存信息的方案，不仅仅低效，而且不方便管理，以及日后的维护也是一个庞大的工作(需要大量的各个部门的人力来维护，当然国家目前已经在完善我们的这个系统了)。

- 这个和我们在应用开发中比较类似：
  - 如果你的状态信息是保存到多个Store对象中的，那么之后的管理和维护等等都会变得特别困难。
  - 所以Vuex也使用了单一状态树来管理应用层级的全部状态。
  - 单一状态树能够让我们最直接的方式找到某个状态的片段，而且在之后的维护和调试过程中，也可以非常方便的管理和维护。

##### 3.1.2 Getters

- 有时候，我们需要从store中获取一些state变异后的状态，比如下面的Store中：
  - 获取学生年龄大于20的个数。![image-20210918112021800](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918112021800.png)

- 我们可以在Store中定义getters

![image-20210918112044461](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918112044461.png)

##### 3.1.3 **Getters作为参数和传递参数**

- 如果我们已经有了一个获取所有年龄大于20岁学生列表的getters, 那么代码可以这样来写

![image-20210918112241995](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918112241995.png)

- getters默认是不能传递参数的, 如果希望传递参数, 那么只能让getters本身返回另一个函数.
  - 比如上面的案例中,我们希望根据ID获取用户的信息

![image-20210918112259602](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918112259602.png)

#### 3.2  Mutation

##### 3.2.1Mutation状态更新

- Vuex的store状态的**更新**唯一方式：**提交Mutation**

- Mutation主要包括两部分：
  - 字符串的**事件类型（type）**
  - 一个**回调函数（handler）**,该回调函数的第一个参数就是state。

- mutation的定义方式：

```vue
mutations:{
	increment(state){
		state.count++
	}
}
```

- 在组件中通过mutation更新

```vue
increment: function(){
	this.$store.commit('increment')
}
```

##### 3.2.2Mutation传递参数（Payload）

- 在通过mutation更新数据的时候, 有可能我们希望携带一些**额外的参数**
  - 参数被称为是mutation的载荷(Payload)

- Mutation中的代码:

![image-20210918113909124](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918113909124.png)

- 但是如果参数不是一个呢?
  - 比如我们有很多参数需要传递.
  - 这个时候, 我们通常会以对象的形式传递, 也就是payload是一个对象.
  - 这个时候可以再从对象中取出相关的信息.

![image-20210918114002750](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918114002750.png)

##### 3.2.3Mutation提交风格

- 上面的通过**commit**进行提交是一种普通的方式

- Vue还提供了另外一种风格, 它是一个包含type属性的对象

```vue
this.$store.commit({
	type:'changeCount',
	count:100
})
```

- Mutation中的处理方式是将整个commit的对象作为payload使用, 所以代码没有改变, 依然如下:

```vue
changeCount(State,payload){
	state.count = payload.count
}
```

##### 3.2.4Mutation响应规则

- Vuex的store中的state是响应式的, 当state中的数据发生改变时, Vue组件会自动更新.

- 这就要求我们必须遵守一些Vuex对应的规则:
  - 提前在store中初始化好所需的属性.
  - 当给state中的对象添加新属性时, 使用下面的方式:
    - 方式一: 使用Vue.set(obj, 'newProp', 123)
    - 方式二: 用新对象给旧对象重新赋值

- 我们来看一个例子:
  - 当我们点击更新信息时, 界面并没有发生对应改变.

- 如何才能让它改变呢?
  - 查看下面代码的方式一和方式二
  - 都可以让state中的属性是响应式的.

![image-20210918115217424](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918115217424.png)

![image-20210918115224557](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918115224557.png)

##### 3.2.5**Mutation常量类型–** **概念**

- 我们来考虑下面的问题:
  - 在mutation中, 我们定义了很多事件类型(也就是其中的方法名称).
  - 当我们的项目增大时, Vuex管理的状态越来越多, 需要更新状态的情况越来越多, 那么意味着Mutation中的方法越来越多.
  - 方法过多, 使用者需要花费大量的经历去记住这些方法, 甚至是多个文件间来回切换, 查看方法名称, 甚至如果不是复制的时候, 可能还会出现写错的情况.

- 如何避免上述的问题呢?
  - 在各种Flux实现中, 一种很常见的方案就是使用**常量**替代Mutation事件的类型.
  - 我们可以将这些常量放在一个单独的文件中, 方便管理以及让整个app所有的事件类型一目了然.

- 具体怎么做呢?
  - 我们可以创建一个文件: mutation-types.js, 并且在其中定义我们的常量.
  - 定义常量时, 我们可以使用ES2015中的风格, 使用一个常量来作为函数的名称.

![image-20210918141158367](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918141158367.png)

##### 3.2.6Mutation同步函数

- 通常情况下, **Vuex要求我们Mutation中的方法必须是同步方法.**
  - 主要的原因是当我们使用devtools时, 可以devtools可以帮助我们捕捉mutation的快照.
  - 但是如果是异步操作, 那么devtools将不能很好的追踪这个操作什么时候会被完成.

- 比如我们之前的代码, 当执行更新时, devtools中会有如下信息: 图1

- 但是, 如果Vuex中的代码, 我们使用了异步函数: 图2

![image-20210918141459017](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918141459017.png)

- 你会发现state中的info数据一直没有被改变, 因为他无法追踪到.

- **So,** **通常情况下**,不要再**mutation**中进行异步的操作

#### 3.3Action

##### 3.3.1Action的基本定义

- 我们强调, 不要再Mutation中进行异步操作.
  - 但是某些情况, 我们确实希望在Vuex中进行一些异步操作, 比如网络请求, 必然是异步的. 这个时候怎么处理呢?
  - Action类似于Mutation, 但是是用来代替Mutation进行异步操作的.

- Action的基本使用代码如下:

- context是什么?
  - context是和store对象具有相同方法和属性的对象.
  - 也就是说, 我们可以通过context去进行commit相关的操作, 也可以获取context.state等.
  - 但是注意, 这里它们并不是同一个对象, 为什么呢? 我们后面学习Modules的时候, 再具体说.

- 这样的代码是否多此一举呢?
  - 我们定义了actions, 然后又在actions中去进行commit, 这不是脱裤放屁吗?
  - 事实上并不是这样, 如果在Vuex中有异步操作, 那么我们就可以在actions中完成了.![image-20210918142835510](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918142835510.png)

##### 3.3.2Action的分发

- 在Vue组件中, 如果我们调用action中的方法, 那么就需要使用dispatch

- 同样的, 也是支持传递payload![image-20210918143045646](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918143045646.png)

##### 3.3.3Action返回的Promise

- 前面我们学习ES6语法的时候说过, Promise经常用于异步操作.
  - 在Action中, 我们可以将异步操作放在一个Promise中, 并且在成功或者失败后, 调用对应的resolve或reject.

- OK, 我们来看下面的代码:

![image-20210918143717446](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918143717446.png)

#### 3.4认识Model（可以看看实例）

##### 3.4.1认识Module

- Module是模块的意思, 为什么在Vuex中我们要使用模块呢?
  - Vue使用单一状态树,那么也意味着很多状态都会交给Vuex来管理.
  - 当应用变得非常复杂时,store对象就有可能变得相当臃肿.
  - 为了解决这个问题, Vuex允许我们将store分割成模块(Module), 而每个模块拥有自己的state、mutation、action、getters等

- 我们按照什么样的方式来组织模块呢? 
  - 我们来看下边的代码![image-20210918143941469](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918143941469.png)

##### 3.4.2Module局部状态

- 上面的代码中, 我们已经有了整体的组织结构, 下面我们来看看具体的局部模块中的代码如何书写.
  - 我们在moduleA中添加state、mutations、getters
  - mutation和getters接收的第一个参数是局部状态对象

- 注意:
  - 虽然, 我们的doubleCount和increment都是定义在对象内部的.
  - 但是在调用的时候, 依然是通过this.$store来直接调用的.

![image-20210918144646742](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918144646742.png)

##### 3.4.3Actions的

- actions的写法呢? 接收一个context参数对象
  - 局部状态通过 context.state 暴露出来，根节点状态则为 context.rootState
  - ![image-20210918144822523](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918144822523.png)

- 如果getters中也需要使用全局的状态, 可以接受更多的参数![image-20210918144838893](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918144838893.png)

#### 3.5项目结构

-  当我们的Vuex帮助我们管理过多的内容时, 好的项目结构可以让我们的代码更加清晰.![image-20210918145107353](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210918145107353.png)

## 第七篇：网络模块 axios

### 1.如何选择网络模块

- Vue中发送网络请求有非常多的方式, 那么, 在开发中, 如何选择呢?
  - 选择一: 传统的Ajax是基于XMLHttpRequest(XHR)

- 为什么不用它呢?
  - 非常好解释, 配置和调用方式等非常混乱.
  - 编码起来看起来就非常蛋疼.
  - 所以真实开发中很少直接使用, 而是使用jQuery-Ajax

- 选择二: 在前面的学习中, 我们经常会使用jQuery-Ajax
  - 相对于传统的Ajax非常好用.

- 为什么不选择它呢?
  - 首先, 我们先明确一点: 在Vue的整个开发中都是不需要使用jQuery了.
  - 那么, 就意味着为了方便我们进行一个网络请求, 特意引用一个jQuery, 你觉得合理吗?
  - jQuery的代码1w+行.
  - Vue的代码才1w+行.
  - 完全没有必要为了用网络请求就引用这个重量级的框架.

- 选择三: 官方在Vue1.x的时候, 推出了Vue-resource.
  - Vue-resource的体积相对于jQuery小很多.
  - 另外Vue-resource是官方推出的.

- 为什么不选择它呢?
  - 在Vue2.0退出后, Vue作者就在GitHub的Issues中说明了去掉vue-resource, 并且以后也不会再更新.
  - 那么意味着以后vue-reource不再支持新的版本时, 也不会再继续更新和维护.
  - 对以后的项目开发和维护都存在很大的隐患.

- 选择四: 在说明不再继续更新和维护vue-resource的同时, 作者还推荐了一个框架: axios为什么不用它呢?
  - axios有非常多的优点, 并且用起来也非常方便.
  - 稍后, 我们对他详细学习.

### 2.axios

#### 2.1为什么选择axios？

1. n为什么选择axios? 作者推荐和功能特点、

   ![image-20210919083729863](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919083729863.png)

2. n功能特点
   - 在浏览器中发送 XMLHttpRequests 请求
   - 在 node.js 中发送 http请求
   - 支持 Promise API
   - 拦截请求和响应
   - 转换请求和响应数据

#### 2.2axios请求方式

- 支持多种请求方式:
  - axios(config)
  - axios.request(config)
  - axios.get(url[, config])
  - axios.delete(url[, config])
  - axios.head(url[, config])
  - axios.post(url[, data[, config]])
  - axios.put(url[, data[, config]])
  - axios.patch(url[, data[, config]])

##### 2.2.1发送get请求演示

![image-20210919084156419](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919084156419.png)

##### 2.2.2**发送并发请求**

- 有时候, 我们可能需求同时发送两个请求
  - 使用axios.all, 可以放入多个请求的数组.
  - axios.all([]) 返回的结果是一个数组，使用 axios.spread 可将数组 [res1,res2] 展开为 res1, res2

![image-20210919084252072](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919084252072.png)

##### 2.2.3全局配置

- 在上面的示例中, 我们的BaseURL是固定的
  - 事实上, 在开发中可能很多参数都是固定的.
  - 这个时候我们可以进行一些抽取, 也可以利用axiox的全局配置

![image-20210919084804676](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919084804676.png)

##### 2.2.4常见的配置选项

- 请求地址
  - url: '/user',

- 请求类型
  - method: 'get',

- 请根路径
  - baseURL: 'http://www.mt.com/api',

- 请求前的数据处理
  - transformRequest:[function(data){}],

- 请求后的数据处理
  - transformResponse: [function(data){}],

- 自定义的请求头
  - headers:{'x-Requested-With':'XMLHttpRequest'},

- URL查询对象
  - params:{ id: 12 },

- 查询对象序列化函数
  - paramsSerializer: function(params){ }

- request body
  - data: { key: 'aa'},

- 超时设置s
  - timeout: 1000,

- 跨域是否带Token
  - withCredentials: false,

- 自定义请求处理
  - adapter: function(resolve, reject, config){},

- 身份验证信息
  - auth: { uname: '', pwd: '12'},

- 响应的数据格式 json / blob /document /arraybuffer / text / stream
  - responseType: 'json',

### 3.axios实例

- 为什么要创建axios的实例呢?
  - 当我们从axios模块中导入对象时, 使用的实例是默认的实例.
  - 当给该实例设置一些默认配置时, 这些配置就被固定下来了.
  - 但是后续开发中, 某些配置可能会不太一样.
  - 比如某些请求需要使用特定的baseURL或者timeout或者content-Type等.
  - 这个时候, 我们就可以创建新的实例, 并且传入属于该实例的配置信息.

![image-20210919085316899](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919085316899.png)

**axios封装**

![image-20210919085336372](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919085336372.png)

### 4.拦截器

#### 1.**如何使用拦截器？**

- axios提供了拦截器，用于我们在发送每次请求或者得到相应后，进行对应的处理。

- 如何使用拦截器呢？

![image-20210919085539423](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919085539423.png)

#### 2.拦截器中都做了什么？

- 请求拦截可以做到的事情：

![image-20210919085947460](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919085947460.png)

- 请求拦截中错误拦截较少，通常都是配置相关的拦截

- 可能的错误比如请求超时，可以将页面跳转到一个错误页面中。

4.3.拦截器中都做了什么？

- 响应拦截中完成的事情：
  - 响应的成功拦截中，主要是对数据进行过滤。

![image-20210919090102889](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919090102889.png)

- 响应的失败拦截中，可以根据status判断报错的错误码，跳转到不同的错误提示页面。

![image-20210919090122089](https://gitee.com/hzg-sss/typora-picture/raw/master/img/image-20210919090122089.png)

## 知识点补充

### 1.高阶函数

#### 1.1filter，map，reduce

##### 1.1.1filter函数的使用：

- filter中的回调函数有一个要求：必须返回一个boolean值
- true：当返回true时，函数的内部会自动将这次回调的n加入到新的数组中
- false：当返回false时，函数的内部会过滤掉这次的n

```vue
<script text="javascript">
        const nums = [10, 20, 30, 40, 50, 91, 73, 50]

        let newNums = nums.filter(function(n) {
            return n < 100
        })
        console.log(newNums);
    </script>
```

##### 1.1.2map函数的使用：

- 让数组中的值都有一次变化的话用**map**（例如：数组中的每一个值都乘以2）

```vue
  let new2Nums = newNums.map(function(n) {
            return n * 2
        })
        console.log(new2Nums);
```

##### 1.1.3.reduce的使用：

- reduce的作用：对数组中的所有值进行汇总、

```vue
//preValue：前面值得累加，有点像sum
            //n：数组中的值，
        let total = new2Nums.reduce(function(preValue, n) {
            return preValue + n;
        }, 0)
        console.log(total);
```

#### 2.箭头函数：

- 箭头函数也是一种定义函数的方式

##### 1.定义函数的方式：function

```vue
const aaa = function(){

}
```

##### 2.对象字面量中定义函数

```vue
const obj = {
	bbb:function(){
	
	},
	bbb(){
	
	}
}
```

##### 3.ES6中的箭头函数

```vue
const ccc = (参数列表)=>{

}
```

```vue
 <script text="javascript">
        //参数问题：
        //1.1放入两个参数
        const sum = (num1,num2)=>{
            return num1+num2
        }

        //1.2放入一个参数(一个参数的时候，参数括号可以省略)
        const power =num=>{
            return num * num
        }

        //2函数代码块有多行代码的时候
        const sss = test=>{
            //1.打印HelloWord
            console.log(HelloWord)
            //2.打印total
            console.log(total)
        }
        //2.1函数代码块有一行代码块的时候   不用写return
        const nul = (num1,num2)=>num1+num2
    </script>
```

#### 3.this的指向问题

在非箭头函数下， this 指向调用其所在函数的对象，而且是离谁近就是指向谁（此对于常规对象，原型链， getter & setter等都适用）；构造函数下，this与被创建的新对象绑定；DOM事件，this指向触发事件的元素；内联事件分两种情况，bind绑定， call & apply 方法等， 容以下一步一步讨论。箭头函数也会穿插其中进行讨论。

##### 3.1全局环境下：

在全局环境下，this 始终指向全局对象（window）, 无论是否严格模式；

```vue
console.log(this.document === document); // true

// 在浏览器中，全局对象为 window 对象：
console.log(this === window); // true

this.a = 37;
console.log(window.a); // 37
```

##### 3.2函数直接调用

普通函数内部的this分两种情况，严格模式和非严格模式。

非严格模式下，this 默认指向全局对象window

```vue
function f1(){
  return this;
}

f1() === window; // true
```

而严格模式下， this为undefined

```stylus?linenums
function f2(){
  "use strict"; // 这里是严格模式
  return this;
}

f2() === undefined; // true
```

##### 3.3对象中的this

对象内部方法的this指向调用这些方法的对象，

1. 函数的定义位置不影响其this指向，this指向只和调用函数的对象有关。
2. 多层嵌套的对象，内部方法的this指向离被调用函数最近的对象（window也是对象，其内部对象调用方法的this指向内部对象， 而非window）。

```vue
<script text="javascript">
//1
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};
console.log(o.f());  //37
var a = o.f;
console.log(a()):  //undefined

var o = {prop: 37};

function independent() {
  return this.prop;
}

o.f = independent;

console.log(o.f()); // logs 37

//2
o.b = {
  g: independent,
  prop: 42
};
console.log(o.b.g()); // logs 42
</script>
```

##### 3.1箭头函数中的this

箭头函数中的this引用的是最近作用域中的this













































上周总结：

- 上周在做前后端分离的作品，在做前端页面的时候，发现很多的vue的知识点遗忘了，于是复习总结了一波vue，将vue详细的进行一次归纳。在归纳的过程中，又学到很多。
- 最近学习的效率极低，用了三天的时间将vue全部过了一遍，自己的作品搁浅了好几天，
- 课程较多，而且有几门课很重要，必须好好地听讲并课后在看看相关的视频来巩固自己的学习，把基础打好点。

问题：

- 现阶段的心里，比较的迷茫，感觉这一阶段学的真的很累，虽然知道学什么，但没有找到如何学，怎样算是现阶段可以了。自己的现阶段该了解什么样的知识，如何开展下一阶段的学习。只知道大体的目标，但中间的实现过程好模糊，好像在黑夜中摸着行走。知道往前走，但不知到自己的该如何走，该怎么走，中间有什么东西是可以避免的，有点害怕，想往后看，而不是往前走。
- 最近总是静不下心来，学习比较的浮躁，有学习的枯燥，快回家了，更多的是迷茫学习中遇到的问题。需要自己的克服吧

下周计划：

- 将自己的作品完成，适当复习，巩固完善自己的基础能力。特别是java。
- 较大的经历放在自己得专业课上和数据结构
- 利用课余时间健身，来放松自己
- 调整好心态，好好地学习。

