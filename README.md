## demo1：
### 需求内容
1. 输入数值左右移动
2. 可以撤销和前进

### 模块设计：

1. 操作指令输入模块
2. 操作div模块
3. 撤销和前进模块
4. 状态管理模块

### 数据驱动思想
#### 根据事件
view:事件驱动->操作dom
#### 根据数据
data:事件触发->操作数据->映射器->操作dom

#### 命令模式

含义：把具体的指令与实现隔离，对调用与执行解耦

做法：将方法、数据都封装到单一的对象中，对调用方与执行方进行解耦，达到职责分离的目的

解决的问题：
1. 不知道调用哪个api
2. 调用的api复杂
3. 不知道应该交给哪个对象执行

例子：客户-服务员-厨师 


#### 策略模式
将方法封装为对象属性

```javascript
var state = {
                            front: function () {
                                DataMangerOb.back(handler);
                                changeDiv(DataMangerOb);
                            },
                            back: function () {
                                DataMangerOb.front(handler);
                                changeDiv(DataMangerOb);
                            }
                        };
                        state[handler]();
```



## demo2

### 需求

1. 实现画廊效果
2. 图片数量由后端数据指定，排列顺序不一定
3. 每个图片下面有该图片的下标                        

### 分析

数据驱动，分析模块
模块设计原则：**低耦合**，针对需求，方便扩展
模块列表：
1. 生成dom
2. 渲染dom
3. 命令解析

#### 设计模式
##### 适配器模式

```javascript
//各大框架使用的内容--与默认指令合并
        //1.默认指令，不需要用户输入
        //2.防止漏输入
        var final = {};
        var defaultHandler = {
            data: [],
            id: document,
            way: 'normal',
            size: [100, 100]
        }
        //合并配置
        for (var item of defaultHandler) {
            if (handler[item]) {
                final[item] = handler[item];
                if (item === 'id') {
                    final.id = document.getElementById(item)
                }
            } else {
                final[item] = defaultHandler[item]
            }
        }
        return final;
```


##### 享元模式
题外话：使用函数柯里化

```javascript
styleArr.forEach((style, index) => {
                switch (index) {
                    case 0:
                        handlerDom=div
                        break
                    case 1:
                        handlerDom=span
                        break  
                    case 1:
                        handlerDom=img
                        break 
                    default:

                }
                for(var item in style){
                    handlerDom.style[item]=style[item]
                }
            })

```