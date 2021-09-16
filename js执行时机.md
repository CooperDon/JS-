### 《JS函数的执行时机》

##### 关于JS任务执行

> ​	众所周知，JS是一门单线程语言。那就像我们去银行办理业务，而单线程意味着只有一个办理窗口，那么每个人都要等前一个人办理完成后，再去办理。同理JS也是一样，JS任务要一个一个按顺序执行。那么问题来了，如果前一个任务执行时间过长，后一个任务也要等着，这样必然增加了网页的加载时间。因此聪明的程序员将任务分成两类。

+ 同步任务：上一件事情没有完成，继续处理上一件事情，只有上一件事情完成了，才会做下一件事情 –> JS中大部分都是同步编程。
+ 异步任务：规划要做一件事情，但是不是当前立马去执行这件事情，需要等一定的时间，这样的话，我们不会等着他执行，而是继续执行下面的操作。

##### JS 函数的执行时机

>  	函数执行的时机不同，运行结果也不同。下面我们按同步任务和异步任务两种情况，分别解释函数执行时机。

###### 同步

```javascript
let a = 1
function fn() {console.log(a)}		//a undefined
```

执行步骤：

1. 声明变量a并赋值为1
2. 声明函数fn
3. 结束

###### 异步

```javascript
let a = 1
function fn(){
    setTimeout(()=>{console.log(a)},0)
}
fn() // 2
a = 2
```

执行步骤：

1. 声明变量a并赋值为1
2. 声明函数fn
3. 执行fn() –> setTimeout()会过一会执行 –>跳过setTimeout()
4. 将2赋值为a
5. 执行setTimeout() //打印出a
6. 结束

```javascript
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}

//for循环执行步骤：
//i赋值为0
//判断i < 6 ?,满足进入第一循环
//setTimeout()会过一会执行–>跳过setTimeout()继续执行
//执行i++，此时i的值为1
//判断i < 6 ?,满足进入第二循环
//setTimeout()会过一会执行–>跳过setTimeout()继续执行
//执行i++，此时i的值为2
//省略…
//执行i++，此时i的值为6
//判断i < 6 ?,不满足跳出循环
//执行第一次循环的setTimeout() //打印出a
//执行第二次循环的setTimeout() //打印出a
//执行第三次循环的setTimeout() //打印出a
//执行第四次循环的setTimeout() //打印出a
//执行第五次循环的setTimeout() //打印出a
//执行第六次循环的setTimeout() //打印出a
//结束
//现在可以看出，由于setTimeout()的执行时间为for语句执行后，所以每次打印出的结果都为6
```

###### 打印0、1、2、3、4、5

```javascript
for(let i = 0; i<6; i++){
    setTimeout(()=>{
        console.log(i)
    },0)
}

//或利用闭包
let i 
for(i = 0; i<6; i++){
  !function(j){
      setTimeout(()=>{
        console.log(j)
      },0)
  }(i)
}
```

