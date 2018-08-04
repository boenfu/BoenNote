根据

[TypeScript入门课程 --慕课网](http://www.imooc.com/learn/763)

整理，提取 的笔记

半数视频内容讲解的是 ES6 知识 没有详细记录



<!-- more -->

#### 1.字符串模板

\`多行${变量}字符串\` 

 ```
   function test（arry,a,b);
   //字符串模板使用
   
   test `Hello #{4},and #{5}!`
  
   //第一个参数是被变量切开的字符串数组
   
   ["Hello ",",and ","!"]
   
   //第二个变量a=4，
   // 第三个变量b=5
   // --就是 es6 里面那个
 ```



#### 2.变量类型

 赋值类型 赋值后变了在 ts 会报错 编译成 js 不会

 var myname:string = "boen";

   变量后面有： string any number boolean 等

   function test（）：void{}  表示没有返回值 

   ```
   //自定义类型
   class Person{
       name: string,
       age: number
   }
   var xiaofu: Person = new Person();
   xiaofu.age = 20;
   ```





#### 3.函数参数

ts里面 函数 参数没传够会报错，

指定了类型没传对也会报错，设了默认值就不会

参数名后，冒号前加 ? 表示是可选参数



#### 4.任意操作符

 ...任意参数符 --es6里那个



#### 5.生成器函数

 生成器函数 generation --es6那个

yield



#### 6.析构表达式

针对对象的：

```
function test(){
return {
	a:1,
	b:{
        c: 2
	}
	}
}

//名字得一样 因为是省略写法 {a:a,b:b} 键是参数名值
//要想直接取c的话可以嵌套 {a,b:{c}}
var {a,b} = test();

例：
var {a,b:{c:sb}} = t();
console.log(a,sb);返回的只有a和sb，sb是c的值

```

针对数组的：

用 []



#### 7.箭头函数

--es6里看的那个

 方法体只有一行的话不用 {} 也不用 return；

给对象原型新增方法时别用箭头函数，因为this的关系，得不到上下文



#### 8.for..of

ts 里给数组声明属性是会报错的

对比：

arry.foreach() 1.中途不能用 break 之类的跳出去 2.会忽略属性值

for..in 遍历的是键

for of 可以break，默认遍历的是值（可以设置遍历键值对或键--es6里看的那个）



### 9.类

--这里是干货了

```
//就像JAVA一样
//有点跟java不一样 ts默认是public 一共三种，java 默认的是同包下可用 四种
//声明类
class Person{

	//这个就相当于Java的构造函数
	constructor(){
        
	}

	//受保护的，类内部和子类可用
    protected money；
    
    //默认public
    public name；
    
    //内部可访问
    private say(){
        console.log(name);
    }
}


```

注：重要

​	如果构造函数里面要给属性赋初始值，new的时候就必须传

​	如果构造函数要赋值的属性还没定义，就必须要指定类型 如 constructor(public age:number)



### 10.类 -继承

和 java 类似

```
class Boen extends Person{
    //会得到父类的属性，方法
}
```

super 两个用法

1.子类的要写构造函数的时候，必须在构造函数里面调用父类的构造函数

 例 ： super(name);

2.调用父类方法

例： super.say(); //这个例子不准确，因为上面的say是private



### 11.泛型

```
var Worker：Array<Person> = [];
//ta和ta的子类都是能放进去的 其他会错
Woker[0] = new Person("xx");
Woker[1] = new Boen("bb");
```



### 12.接口

要点1：

当在类构造器里声明变量类型为一个接口时，必须传入该接口的所有属性

```
interface a{
    name:string;
}
class Person{
    constructor(public config: a){
        
    }
}
new Person({
    name: "boen"
})
```

要点2：

类继承接口时，必须实现所有接口的方法 --跟 java 一样

```
class b implements a{
    
}
```



### 13.模块

就是node或者说es6里面用的 export 和 import

```
export var aaa；

import {aaa} from xxx

注 额外：
export default 可以不写大括号
但是一个文件只能有一个 export default
```



### 14.注解

主要用于告诉框架 如 angular 怎么去处理这个类



### 15.类型定义文件

用于 ts 加载如已有 js 库的配置文件

.d.ts后缀

GitHub上 typings 里有常用框架的配置文件

