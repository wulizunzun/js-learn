# 设计模式

* 设计原则

    - 单一职责原则（SRP）

        - 一个对象或方法只做一件事情
        - 如果一个方法承担了过多的职责，那么在需求变迁过程中，需要改写这个方法的可能性就越大

    - 最少知识原则（LKP）

        - 一个软件实体应当尽可能少地与其他实体发生相互作用 
        - 应当尽量减少对象之间的交互。如果两个对象之间不必彼此直接通信，那么这两个对象就不要发生直接的 相互联系，可以转交给第三方进行处理
    
    - 开放-封闭原则（OCP）

        - 软件实体（类、模块、函数）等应该是可以 扩展的，但是不可修改
        - 当需要改变一个程序的功能或者给这个程序增加新功能的时候，可以使用增加代码的方式，尽量避免改动程序的源代码，防止影响原系统的稳定

* 创建型模式

    - 单例模式  

        - 定义 ：保证一个类仅有一个实例，并提供一个访问它的全局访问点
        - 核心 ：确保只有一个实例，并提供全局访问
        - 实现 ：
        
            ```javascript
                function SetManager(name) {
                    this.manager = name;
                }

                SetManager.prototype.getName = function() {
                    console.log(this.manager);
                };

                // 提取出通用的单例
                function getSingleton(fn) {
                    var instance = null;

                    return function() {
                        if (!instance) {
                            instance = fn.apply(this, arguments);
                        }
                        return instance;
                    }
                }

                // 获取单例
                var managerSingleton = getSingleton(function(name) {
                    var manager = new SetManager(name);
                    return manager;
                });

                managerSingleton('b').getName(); // b
                managerSingleton('c').getName(); // b
            ```

    