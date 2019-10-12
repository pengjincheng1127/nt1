# 第一天
### git与github

> git 版本控制工具

SVN：集中式
    弊端:版本控制必须需要网络支持，一般SVN都是局域网，只能是公司内部人员使用，外界的人想参与开发是比较麻烦的，中央服务器不一定就稳定，一旦出事中央服务器所有资源都洗白白。

GIT：分布式
    不需要网络支持就能进行版本控制，只要能上网还要有开发权限都能参与开发，就算远程仓库库出事儿，计算机已经有了历史记录

GITHUB：程序员交友网站、远程仓库、帮助学习


> git的三大区域

- 工作区 （本地）

- 暂存区 （保护工作区和版本区）

- 版本区 （版本库、历史区）只有行成版本才能进行版本的控制


- 形成版本就是根据.git文件来操作的，所以说要进行版本控制，必须要有.git这个隐藏文件

- 按着tab键可以补全命令

- 设置用户信息:

git config --global user.name 'xxx'
git config --global user.eamil 'xxx'

- 创建版本仓库
    git init(想在哪进行版本控制，就在哪个文件夹下使用右键点击git bash here)


- 查看状态
    - git status

    如果查看状态的时候发现文件是红色的，就说明文件没有进行版本控制

- 工作区到暂存区
    - git add 文件名
    - git add .  (快速把所有文件都放到暂存区)


- 暂存区到版本区
    - git commit -m "取个自己能够识别的名字"


- 快速从工作区到版本区
    - git commit -a -m "取个自己能够识别的名字"

- 查看版本
    - git log
    - git reflog (查看所有的历史记录（包括历史区回滚后）)

出现nothing to commit, working directory clean就说明没有文件没被管理了（都被管理了）


- 回滚
    git reset --hard 历史ID


- touch .gitignore (创建.gitignore文件)

在文件中填写过滤的文件或文件夹

*.zip、*.rar、*.via、*.tmp过滤这些后缀名的文件

排除指定文件夹下的文件， /txt/1.txt

排除指定文件夹  \txt2

git rm -r --cached .  如果已经提交过的代码，使用.gitignore是无效的，那么请使用前面这段代码


- clear清屏

- 如果发现:号就按Q键退出

- 查看各大区域的区别
    - 工作区到暂存区  git diff
    - 工作区到版本区  git diff master
    - 暂存区到版本区  git diff --cached


- 把本地git的版本上传到github上管理

    - 设置秘钥:
        ssh-keygen -t rsa -C "your_email@example.com"

    - 登录github，右边头像下拉列表有个settings，找到SSH and GPG keys，找到new ssh key点击，把秘钥放到文本框中，点击add ssh key。

    - 在github上创建一个项目
        - 加号下拉列表，第一个创建新项目
        - 仓库名称
        - 说明
        - 公开
        - README打钩

- 查看远程仓库
    - git remote -v   
- 创建远程仓库
    - git remote add origin 远程地址
    ```
       比如: git remote add origin git@github.com:nizp/2019-10-8.git
    ```

- 同步远程
    - git pull origin master

- 推送到远程
    - git push origin(远程名字) master(分支名)
    ```
        比如:git push origin master
    ```
- 删除远程仓库
    - git remote remove 远程名字


- 克隆项目
    - 找到远程仓库的地址，git clone远程仓库地址 回车



### node的安装（自带就有npm）

- 项目的初始化
    - npm init -y
- npm install 安装程序

- npm uninstall 删除安装程序

- npm 目前是全球最大的包管理平台（里面有很多的代码资源）

npm install nrm -g

- 测nrm的速度  
    - nrm test
- 切换资源路线
    - nrm use taobao

- yarn的安装
    - npm install yarn -g

    - yarn add 安装程序
    - yarn remove 要删除的程序

# 第二天

## 作用域（scope）
    运行js的范围

    当打开浏览器的时候，解读到script标签的时候，会把js运行在一个window的全局作用域下（整个window下的环境都叫全局作用域）
    一个变量或者一个函数，默认属于window
    
    在运行函数的时候，函数内部会开辟一个执行栈，在执行栈中会创建一个活动变量的对象，会把函数中所有的变量、函数存储到这个活动变量下，执行栈去运行这个活动变量，这些活动变量下的变量、函数只会作用在函数内，这种现象就叫（局部作用域）

    作用域链：
        如果函数内访问不到某个变量，先去参数中找，还找不到会向父级函数查找，直到window全局，如果还找不到就报错


    局部作用域运行： 
        1.没有形参的时候，但是有var 如果在var的上方访问这个变量，结果是undefined
        2.有形参并且也有实参也有var ，如果在var的上方访问这个变量，结果应该是实参
        3.如果函数内有函数，有形参并且也有实参，那么结果就为函数内的函数 


## 变量提升（预解析机制）
    当浏览器去解析js的时候，会提前解析全局的变量或者函数的过程。

第一步：
    上来就找var和function

第二步：
    逐行解读代码，此时var和function就不用再去读了，一般都的是赋值、计算、输出、判断


    一个匿名函数自执行函数，如果带有名字，在函数体内不管如何赋值同名的变量，结果都等于这个有名函数

PK规则：
    变量没有函数大，后面的函数声明比前面的函数声明大（后面的函数声明会覆盖前面的函数声明）

## 闭包
    
    函数就是一个闭包，   闭包 函数可以使用函数之外定义的变量

    内部函数的作用域链仍然保持着对父函数活动对象的引用，就是闭包（closure）

    函数嵌套函数，子函数引用父函数的参数或者变量，并且子函数还被外界所引用，这个时候子函数的作用域链仍然保持着对父函数活动对象的引用，父函数的参数和变量就不会被浏览器垃圾回收机制给回收，此时打印父函数的函数返回值，会发现在返回值下面有一个scopes，这个scopes下面有个closure，他就是闭包（整个父级都形成了闭包环境）
    

    全局的活动对象在关闭浏览器只会才会被销毁


## let var const 区别

    var 变量提升，存入到全局的活动变量对象中，允许有多个同名的变量，不支持块级作用域

    let 不会变量提升且有暂存死区(在变量定义的上方都访问不到这个变量)
    不会存入到全局的活动变量对象中，
    不允许有多个同名的变量
    支持块级作用域

    const 常量
        不会变量提升且有暂存死区（在变量定义的上方都访问不到这个变量）
        不会存入到全局的活动变量对象中 
        不允许有多个同名的变量
        值是不能被改变的（引用类型可以改变属性值）
        声明了必须赋值


        解决重命名问题一（封闭空间） 也有人看到匿名函数自执行都称为闭包
        函数天生就有局部作用域，函数内的变量、函数或者参数不被外界污染就形成了一个天然的保护层，不会被全局污染

        每个引用类型的地址是不一样的，在不一样的地址下挂同名的属性访问的时候，虽然属性名一样 但是空间地址不一样，也能解决重命名的问题（命名空间）

# 第四天

    全局栈一般是浏览器关闭才会被销毁
    局部栈一般是函数调用完之后被销毁

    堆：引用类型
```js
    let obj = {};
    obj = null ;
    //给obj赋值了一个空指针，谷歌浏览器会在空闲的时候去查看谁用着obj，null指针说明没有使用，所以obj被销毁
```

##  this （小难点）
    
   - 在事件中，事件触发是谁，this就是谁
```js
    document.onclick =function(){
        console.log(this);//document
    }
```

   - 函数直接调用默认this为window
```JS
function(){
        console.log(this);//window
    }
    fn()
```

   - 方法（函数前面有主的都叫方法），this就是.前面的主(箭头函数例外)
      ```js
            let obj = {
                fn:function (){
                    console.log(this);
                }
            }
            obj.fn(); //obj
        ```

   - 箭头函数，他的this为函数定义时的上下文作用域
```js
    document.onclick =function(){
        let fn = ()=>{
            console.log(this);
        }
        fn()
    }

```

## 面向对象(Object,Oriented,OO)

> 面向对象是一种对现实世界理解和抽象的方法，是计算机编程技术发展到一定阶段后的产物。
  
    现实理解(东西是一样的，但是角度不同，所以描述的过程不同)，抽象方法

    抽象：抽离像的部分（归类）

    归类（归纳多种相同的特征

    面向对象是一种编程思想，就是把相同部分的代码抽离出来归为一类，把描述这个类的共有特征（方法或者属性）挂在类的原型下的一种编程思想（方式、模式）

    类的首字母大写
    
### new 
    一元运算符，专门运算函数的，能让函数不加括号的情况下执行，加括号为了传参

    构造函数中的this就是这个构造函数的实例化对象；默认的this也是实例化对象

    return 返回值的如果是简单类型，那么返回的结果为实例化对象，如果返回值为引用类型，那么返回的结果就是这个引用类型


### 原型
>  当一个**函数**创建出来的时候，自身会带有一些属性和方法
    其中有一个属性叫**prototype**,值是对象，他就是原型

    作用：
        构造函数原型下的属性或者方法，只能给函数的实例化对象使用

    原型链：
        __proto__ 只要是实例都有__proto__，而这个原型链是全等于构造函数的原型
        obj.__proto === fn.prototype

    实例下如果有优先实例下的属性或者方法
    通过实例的原型链找到构造函数的原型
    构造函数的原型的原型链找到了Object的原型

    Function 的原型链等于Function的原型

    通过实例调用构造函数原型下的方法，this就是实例

### 单例模式
    单独是实例（实例，具体的事务）。

    由多个简单类型和引用类型组合在一起的事务
```js
      let obj = {
        name:'123';
        sex:'?'
    }
```

    高级单例模式（让单例模式功能更加强大，可以隐藏内部代码，形成模块化编程）
```js
    (function(){
        function hehe(){}
        let obj ={
        name:'123',
        sex:'?'
         }
        return obj
    })()
    o.hehe();//调用

```

    简单类型：
    引用类型：
```js
    //访问对象属性默认就暴露出来了，功能不够强大
    let obj ={
        name:'123',
        sex:'?'
    }
```

### 工厂模式（初始化、加工、出场）

    工厂模式的目的就是为了批量生产对象
 ```js
        function person(name,age,job,sex){
            let obj = new Object(); //初始化(原材料)

            //加工
            obj.name = name;
            obj.age = age;
            obj.job = job;
            obj.sex = sex;

            //出厂
            return obj;
        }

        //obj和obj2就叫实例
        let obj = person('赵炎',15,'前端开发工程师','?'); //批量生产
        let obj2 = person('你真胖',15,'前端开发工程师','?');
```

# 第五天
## 内置类
    内置类就是浏览器自带的一些类这些类都是函数
    Array
    Object
    String
    Boolean
    Number
    Symbol
    Function 

    包装对象：
        在简单类型(排除Null和Undefined)使用属性或者方法的时候，浏览器会偷偷的创建一个内置类的实例，把使用的属性或者方法返回出去之后，这个对象被销毁，这个内置类的实例就叫包装对象

### hasOwnProperty
    for in会枚举原型链,也就是除了对象自身的属性以外，还会查找原型链上的自定义属性
        
        可以通过obj.hasOwnProperty('属性名')去检测某个属性是不是对象自身的
        如果是自身的，就返回true，否则false
### hasPubProperty
    查看属性是不是公共的
```js
   function Fn(){
        this.a = 10;
        this.b = 20;
    }
    Fn.prototype.c = 30;  //公共属性
    let f = new Fn;
    console.log(hasPubProperty(f,'a'));
    function hasPubProperty(obj,attr){
        //如果f能找到c并且c不是f自身的属性，那么就是公共的
        return (attr in obj) && !obj.hasOwnProperty(attr);
    }
```

### call

    为了修改 this 指针
    当一个函数在创建的时候，自身有一些属性和方法，其中有个方法为call
    多个参数
    1.修改this指针
    2.第二个参数之后都是实参

    第一个参数除了null和undefined，别的都是写啥是啥。

### 重写new

    new ：
    函数内的this变成了实例
    默认return实例
