# 设计模式
* 设计原则

    - 单一职责原则（SRP）
        - 一个对象或方法只做一件事情
        - 如果功能特别复杂就进行拆分

    - 最少知识原则（LKP）
        - 一个实体应当尽可能少地与其他实体发生相互作用 
        - 减少对象之间的交互。
        - 如果两个对象之间不必彼此直接通信，那么这两个对象就不要发生直接的 相互联系，可以转交给第三方进行处理

    - 开放-封闭原则（OCP）
        - 对扩展开放，对修改关闭
        - 增加需求时，扩展新代码，而非修改已有代码
        - 这是软件设计的终极目标

* 创建型模式

    - 单例模式  

        - 定义 ：保证一个类仅有一个实例，并提供一个访问它的全局访问点
        - 核心 ：确保只有一个实例，并提供全局访问
        - 实现 ：
            ```javascript
                // es6写法
                class Single {
                    constructor(name){
                        this.name = name;
                    }
                    static getInstance(){
                        if(!this.instance){
                            this.instance = new Single();
                        }
                        return this.instance;
                    }
                }

                // es5写法
                function Window(name){
                    this.name = name;
                }

                function Dialog(title,content){
                    this.title = title;
                    this.content = content;
                }

                Window.prototype.getName = function(){
                    console.log(this.name)
                }

                let CreateSingle = function(Constructor){
                    let instance;

                    return function(){
                        if(!instance){
                            instance = new Constructor(...arguments);
                        }
                        return instance
                    }
                };

                let createWindow = CreateSingle(Window);    
                let W1 = new createWindow('zfpx1');
                let W2 = new createWindow('zfpx2');
            ```

    - 工厂模式

        - 三种工厂模式 
            ```javascript
                class Plant {
                    constructor(name) {
                        this.name = name;
                    }

                    grow() {
                        consolt.log(`我正在生长~~~~`)
                    }
                }

                class Apple extends Plant {
                    constructor(name,flavour){
                        super(name)
                        this.flavour = flavour;
                    }
                }

                class Orange extends Plant {
                    constructor(name,flavour){
                        super(name)
                        this.flavour = flavour;
                    }
                }

                // 直接new的缺点 1.耦合 2.依赖具体的实现

                // 1.简单工厂: 由一个工厂对象决定创建出哪一种产品类的实例 此模式不符合开放封闭原则
                class Factory{
                    static create(type){
                        switch(type){
                            case 'apple' :
                                return new Apple('苹果','甜')
                                break;
                            
                            case 'orange' :
                                return new Orange('橘子','酸')
                                break;
                            
                            default:
                                throw new Error('您要的东西没有~')
                                break;
                        }
                    }
                }
                
                let apple = Factory.create('apple');
                let orange = Factory.create('orange');


                // 2. 工厂方法模式 : 在工厂方法模式中，核心的工厂类不在负责所有的产品的创建，而是将具体的创建工作交给子类去做
                class AppleFactory extends Factory {
                    static create(){
                        return new Apple('苹果','甜');
                    }
                }
                
                let apple = AppleFactory.create();


                // 3.抽象工厂模式
                // 抽象工厂模式是指当有多个抽象角色（产品）时，使用的一种工厂模式
                // 抽象工厂模式可以向客户端提供一个接口，使客户端在不必指定的具体情况下，创建多个产品族中的产品对象 
                class Factory2 {
                    createIcon(){}
                }

                class WindowFactory extends Factory2 {
                    createIcon(){
                        return new WindowIcon();
                    }
                }

                class AppleFactory extends Factory2 {
                    createIcon(){
                        return new AppleIcon();
                    }
                }
                
                class Icon {}
                class AppleIcon extends Icon {
                    render() {
                        console.log('创建苹果图标')
                    }
                }
                class WindowIcon extends Icon {
                    render() {
                        console.log('创建windos图标')
                    }
                }

                let windowFactory = new WindowFactory();
                let appleFactory = new AppleFactory();
                windowFactory.createIcon().render();
                appleFactory.createIcon().render();

                // 总结：
                // 1.简单工厂  函数返回类实例
                // 1.工厂方法  多了工厂类 要想创建产品，需要先创建此工厂的实例，再通过此工厂创建产品
                // 3.在抽象工厂中，一个工厂可以创建多种产品 

            ```


* 结构型模式

    - 代理模式
        - 由于一个对象不能直接引用另外一个对象，所以需要通过代理对象在这两个对象之间起到中介作用
        - 可以在使用者和目标对象间加一个代理对象，通过代理额实现控制
        - 代理模式 vs 装饰器模式 装饰器原来的功能不变还可以使用，代理模式改变原来的功能

            ```javascript
                let wangy = {
                    name : '王燕',
                    age : 31,
                    height : 165
                }

                let wangMaMa = new Proxy(wangy,{
                    get(target,key){
                        if(key === 'age'){
                            return target.age - 2
                        }else if(key === 'height'){
                            return target.height + 3
                        }else{
                            return target[key]
                        }
                    },

                    set(target,key,value){
                        if(key === 'boyFriend'){
                            let boyFriend = value;
                        if(boyFriend.age > 40){
                            throw Error('太老了')
                        }else if(boyFriend.salary < 5000){
                            throw Error('太穷了')
                        }else{
                            console.log("key,",key)
                            target[key] = value
                        }
                    }
                })
                
                wangMaMa.boyFriend = {
                    age : 25,
                    salary:8000
                }
                
                // wangMaMa.age // 29
            ```
        
    - 装饰器模式
        - 在不改变其原有的结构和功能为对象添加新功能
        - 装饰比继承更加灵活

            ```javascript
               // AOP模式：就是在函数执行之前或之后添加一些额外的逻辑，而不需要修改函数的功能
               Function.prototype.before = function(beforeFn){
                    let _this = this;

                    return function(){
                        beforeFn.apply(this,arguments)
                        _this.apply(this,arguments)
                    }
                }

                Function.prototype.after = function(afterFn){
                    let _this = this;

                    return function(){
                        _this.apply(this,arguments)
                        afterFn.apply(this,arguments)
                    }
                }

                function buy(money,goods){
                    console.log(`花${money}元买${goods}`);
                }

                buy = buy.before(function(){
                    console.log("购买东西之前");
                }).after(function(){
                    console.log("函数执行之后");
                }) 

                buy(25,'牛肉')
            ```

    - 策略模式
        - 将定义的一组算法封装起来，使其相互之间可以替换。封装的算法具有一定独立性，不会随客户端变化而变化
        - 避免大量的if else 或者 switch case

            ```javascript
                (function(){
                    let form = {
                        userName : "123",
                        isMobile:13373781946,
                        isEmail:"1204184898@qq.com"
                    }

                    // 策略模式
                    let validator = (function(){
                        // 这是一组规则
                        let rules = {
                            notEmpty(val,msg){
                                if(!val && val !== 0){
                                    return msg
                                }
                            },

                            minLength(val,min,msg){
                                if(!val && val.length < min ){
                                    return msg
                                }
                            },

                            maxLength(val,max,msg){
                                if(!val && val.length > max ){
                                    return msg
                                }
                            },

                            isMobile(val,msg){
                                if(!/^[1][0,3,4,5,6,7,8,9][0-9]{9}$/.test(val)){
                                    return msg
                                }
                            }

                        }

                        let checks = [];

                        // 增加校验的项目
                        function add(value,rule){
                            checks.push(function(){
                                let name = rule.shift()
                                rule.unshift(value)  
                                console.log()
                                return rules[name] && rules[name](...rule)
                            })
                        }

                        function start(){
                            for(let i = 0; i < checks.length; i++){
                                let msg = checks[i]();
                                if(msg){
                                    return msg
                                }
                            }
                        }   

                        function addRule(name,rule){
                            rules[name] = rule
                        }

                        return {
                            add,
                            start,
                            addRule
                        }
                    })()

                    validator.addRule('isEmail',function(val,msg){
                        if(!/^([a-zA-Z]|[0-9])(\w|\-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$/.test(val)){
                            return msg
                        }
                    })
                    validator.add(form.userName,['notEmpty','用户名不能为空'])
                    validator.add(form.isMobile,['isMobile','手机格式不正确'])
                    validator.add(form.isEmail,['isEmail','手机格式不正确'])
                    let msg = validator.start()
                    if(msg){
                        alert(msg)
                        return;
                    }
                    console.log('通过')
                })()
            ```
    - 模板方法
        - 模板方法模式在一个方法定义一个算法的骨架，而将一些步骤的实现延迟到子类中
        - 模板方法使得子类可以在不改变算法结构的情况下，重新定义算法中某些步骤的具体实现
        - 一般有两部分组成，第一部分是抽象父类，第二部分是具体的实现子类
        - 好莱坞原则，子类放弃了控制权，改由父类调用
            - 发布订阅
            - 回调函数

                ```javascript
                    class Parson{
                        dinner(){
                            this.buy();
                            this.cook();
                            this.eat();
                        }

                        buy(){
                            throw new Error('必须由子类实现！');
                        }

                        cook(){
                            throw new Error('必须由子类实现！');
                        }

                        eat(){
                            throw new Error('必须由子类实现！');
                        }
                    }

                    class jiang extends Parson{
                        buy(){
                            console.log('买黄瓜');
                        }

                        cook(){
                            console.log('做黄瓜');
                        }

                        eat(){
                            console.log('吃黄瓜');
                        }
                    }

                    let j = new jiang();
                    j.dinner();
                ```
    
