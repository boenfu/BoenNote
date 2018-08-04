### 《 Learning Typescript 中文版 》 笔记集

#### 1. Typescript 简介

1.变量名后加引号指定类型

2.当一个变量的类型无法推导时，为 any

3.基本类型 boolean number string array void 和自定义enum,它们都是 any 的子类型

4.undefined是全部作用域的一个属性，而null可以看做是一个字面量

5.类型守护

​	如果使用了 typeof 或 instanceof 进行类型检验的话，后续的流程会根据检验结果的类型执行，虽然并不会真正改变变量的类型

```
var x: any = {}
if(typeof x === 'string') {
    console.log(x.splice(3, 1)); //错误 string 没有 splice
}
// x还是any类型
x.foo()
```



6.类型别名

​	使用 type 关键字

​	type boen = number

7.命名空间

​	又称内部模块，能使代码结构更清晰 使用 namespace 定义 内部用 export 导出 见第四章                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               



#### 2. 自动化工作流程

1.tsd 是用来管理 typescript 描述文件的工具，和 npm ， bower一样，它也有自己的配置文件，名为 tsd.json

下载的文件保存在 typings 目录下

// 其余的配置工具 变得太快了 没有精力都弄懂 笔记就略过了



#### 3.使用函数

1.var getName: (id: number) => string 

​	声明一个变量的类型为 （输入id为数字的参数 返回字符串）的一个函数



2.调用函数时传的参数数量与定义时不同会报错

​	解决办法： 在定义时的参数名后加 ? 表示该参数可选

​	可选参数列表 必须位于必选参数后面

3.声明参数默认值 bar: number = 666

​	默认参数列表 也必须位于必选参数后面

​	注： 这里的默认值转为 js 后编译器是通过 if 判断参数是否等于 void 0 来判断是否应用默认的值

​	实际上 void 任何值都是返回 undefined

4.剩余参数 ...foo: number[] 

​	一个剩余参数必须包含一个数组类型

​	建议也放参数列表的尾部

5.函数的重载

​	重载的意思 就是使用相同的名称 和 不同的参数数量 创建多个方法的一种能力

```
function test(name: string) :string  // 重载签名
function test(age: number) :string  // 重载签名
function test(single: boolean) :string  // 重载签名

function test(boen: (string | number | boolean)) :string {
    switch(typeof boen) {
        case 'string':
        	return `我的名字是 ${boen}.`
        case 'number':
        	return `我今年 ${boen} 岁`
        case 'boolean':
        	return boen ? '我还是单身狗 呜呜呜':'我居然能脱单'   
    }
}  // 实现签名
```

​	

所有重载签名必须兼容 如果一个返回数字 另外一个返回字符串 会发生编译错误

实现签名必须兼容所有重载签名

6.特定重载签名

用来创建相同参数，名称 但返回类型不同的多个函数

特点的签名为一个字符串

```
function test(tag: "div"): HTMLDivElement  // 特定重载签名
function test(tag: "span"): HTMLSpanElement  // 特定重载签名
function test(tag: string): HTMLElement  // 非特定重载签名
```

当声明特定签名的时候 至少要包含一个非特定签名 且要在最后列出



7.函数作用域

垃圾回收器会在变量脱离作用域的时候清理掉他们



8.泛型

```
function getList<T>(url: string, cb: (list: T[]) => void): void {
    ...
}
```

​	定义了一个泛型函数

接受一个字符串和一个回调函数 回调函数的参数必须是<>里指定的类型的数组



9.tag 函数 和标签模板

```
var html = htmlEscape `<h1>${boen}</h1>`
// htmlEscape 是个函数 就称为 tag函数
// 后面跟的 模板字符串就变成了标签模板

// htmlEscape 函数如下
function htmlEscape (a, ...b){
    ...
}
// a是静态字面量的数组 在这儿就是 ['<h1>', '</h1>']
// b 是里面的变量的数组 在这儿就是 [boen]
```



10. TypeScript 编译箭头函数时 会干这个 var _this  =  this 然后后面就用 \_this

11.promise 生成器 略

12.异步函数 async 和 await

​	编译为 js 时，es6会用promise来实现，否则使用promise的兼容版本实现

```
var p: Promise <number> = /* ... */
async function fn(): Promise<number> {
    var i = await p;
    return 1 + i;
}
//  调用fn 的时候 会在 await 处等待执行结果
```

2018年7月28日13:50:03





#### 4.Typescript中的面向对象编程

1.关联，聚合和组合

​	关联：有联系但他们的对象有独立的生命周期并且没有从属关系 如老师和学生

​	聚合：有独立生命周期但是有从属关系，切且子对象不能从属于其他对象 如 手机和电池

​	组合：没有独立生命周期 父对象删除后子对象也被删除 如 问题和答案（生命周期依赖其他对象的对象 也被称为若实体 如答案）