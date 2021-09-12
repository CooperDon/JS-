#### 《JavaScript对象基本语法》

##### 对象声明

+ 定义

  + 无序的数据集合(数组)
  + 键值对的集合

+ 基本格式

  ```javascript
  let obj = {
      'name':'frank',
      'age':18
  }
  let obj = new Object({'name':'frank'})
  
  
  //获取对象的属性名
  Object.keys(obj)
  
  
  //使用变量作为key时
  let a= 'xxx'
  let obj = {
      [a] : 'xxxx'
  }
  ```

+ JS中的隐藏属性

  + 每个对象都有一个隐藏属性
  + 隐藏属性的值存放着其共有属性组成的对象的地址
  + 共有属性组成的对象叫做原型
  + <img src="https://i.loli.net/2021/09/12/8jZqPNFvIS3cuks.png" alt="x" style="zoom: 33%;" />

##### 删除对象属性

```javascript
//只删除属性值
obj.name = undefined

//只删除属性值以及属性名
delete obj.xxx
delete obj['xxx']
```

##### 查看对象属性

```javascript
var obj = {'name':'frank','age':18}

//查看对象的属性名
Object.keys(obj)
["name", "age"]

//查看对象的属性值
Object.values(obj)
["frank", 18]

//同时查看
Object.entries(obj)
[Array(2), Array(2)]
0: (2) ["name", "frank"]
1: (2) ["age", 18]

//查看共有对象的共有属性
console.dir(obj)
obj.__proto__

//查看对象是自身属性还是共有属性
obj.hasOwnProperty(toString)
false
```

##### 修改/增加对象属性

```javascript
//直接赋值
let obj = {'name','tony'}
obj.name = 'frank'
obj['name'] = 'tom'

//批量赋值
Object.assign(obj,{'gender':'female','hobby':'running'})
{name: "frank", age: 18, gender: "female", hobby: "running"}

//无法通过自身修改或增加改变共有属性
obi.toString = 'xxx'
obj2.toString	//function

obj.__proto__.toString = 'xxx'
obj2.toString //'xxx'
window.Object.prototype
```

##### 'name' in obj和 obj.hasOwnProperty('name')的区别

+ 两者都可以查看name是否为obj对象的属性
+ 'name' in obj无法判别该name属性是自身属性还是共有属性
+ obj.hasOwnProperty('name')可以解决如上问题
