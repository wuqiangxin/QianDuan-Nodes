# JavaScript高级第01天笔记

## 1. 面向过程与面向对象

（02-面向对象编程介绍.avi）

### 1.1面向过程  ***

- 面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。
- **总结**：按照步骤编程  （函数和变量）

### 1.2面向对象 ***(知道)

- 面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。
- **总结**：将需求分析出一个一个的对象，然后在分析出对象中的属性和方法，最后按照步骤编程（方法和属性）

### 1.3面向过程与面向对象对比

|      | 面向过程                                    | 面向对象                                     |
| ---- | --------------------------------------- | ---------------------------------------- |
| 优点   | 性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程。 | 易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护 |
| 缺点   | 不易维护、不易复用、不易扩展                          | 性能比面向过程低                                 |

### 1.4 应用场景

- 比较简单的逻辑，使用面向过程，前端更偏向使用面向过程。
- 比较复杂的逻辑，使用面向对象，后端更偏向使用面向对象。

## 2. 对象与类 ***

（03-类和对象.avi）

### 2.1 对象

对象是由属性和方法组成的：是一个无序键值对的集合,指的是一个具体的事物

- 属性：事物的特征，在对象中用属性来表示（常用名词）
- 方法：事物的行为，在对象中用方法来表示（常用动词）

### 2.2 类

#### 2.2.0 类介绍

- 在 ES6 中新增加了类的概念，可以使用 class 关键字声明一个类，之后以这个类来实例化对象。

- 类抽象了对象的公共部分，它泛指某一大类（class）对象特指某一个，通过类实例化一个具体的对象

- 类，对象，面向对象**总结：**

  **类**抽象了对象的公共部分，它泛指某一大类（class） 

  **对象**特指某一个，通过类实例化一个具体的对象 

  **面向对象**的思维特点:  

  1. 抽取（抽象）对象共用的属性和行为组织(封装)成一个类(模板) 
  2. 对类进行实例化, 获取类的对象
     1. 实例：实际的例子，对象
     2. 实例化：通过类的构造函数，来创建对象，实例

#### 2.2.1 创建类  

（04-创建类和生成实例.avi）

```js
//步骤1 定义类：使用class关键字
class name {
  // class body
}     
//步骤2 创建实例：使用定义的类创建实例  注意new关键字
var xx = new name();     
```

例子：

```js
// 1. 创建类 class  创建一个 明星类
class Star {
}

// 2. 利用类创建对象 new
var ldh = new Star();
```

问题：

但是这么创建的对象，没有属性和方法呀，怎么办？

需要用到**构造函数**。

#### 2.2.2 类创建添加属性和方法

##### 1. 构造函数介绍

- constructor() 方法是类的构造函数(默认方法)，用于传递参数,返回实例对象
- 通过 new 命令生成对象实例时，自动调用该方法
- 如果没有显示定义, 类内部会自动给我们创建一个constructor() 
- **构造函数的作用：给对象添加（构造）属性**

##### 2. 构造函数添加属性

- 语法：

```js
//步骤1 在类中定义构造函数constructor，函数名固定
class Person {
  constructor(name,age) {//定义形参
      this.name = name;//将形参赋值给this对象的对应属性
      this.age = age;
    }
}       

//步骤2 在实例化对象的时候，传递实参
var ldh = new Person('刘德华', 18); //这里的实参默认传递给Person类中的constructor
console.log(ldh.name);//刘德华
```

**注意事项:**

1. 通过class 关键字创建类，类名我们还是习惯性定义首字母大写
2. 类里面有个constructor 函数，可以接受传递过来的参数，同时返回实例对象
3. constructor 函数 只要 new 生成实例时，就会自动调用这个函数，如果我们不写这个函数,类也会自动生成这个函数
4. 生成实例 new 不能省略
5. 语法规范, 创建类 类名后面不要加小括号,生成实例 类名后面加小括号, 构造函数不需要加function

##### 3. 类中添加方法  

（05-类中添加共有方法.avi）

- 语法

```js
//步骤1 添加普通方法
class Person {
  constructor(name,age) {  
      this.name = name;
      this.age = age;
      this.btn = ...
      this.btn.onclick = this.say;
      // this.btn.onclick(); --- this.btn.say()
       this.btn.onclick = function(){
    
         console.log(this.name + '你好');
    }
    }/------------------------------------------->注意,方法与方法之间不需要添加逗号
   say() {
      console.log(this.name + '你好');
   }
var say = function(){
    
     console.log(this.name + '你好');
}
}       

//步骤2  通过对象调用方法
var ldh = new Person('刘德华', 18); 
ldh.say()   
```

**注意事项**：        

1. 我们类里面所有的函数不需要写function 
2. **多个函数方法之间不需要添加逗号分隔**



#### 2.2.3 类的继承 

（06-类继承extends和super关键字.avi）

- 现实中的继承：子承父业，比如我们都继承了父亲的姓。 
- 程序中的继承：子类可以继承父类的一些属性和方法。
- **类的继承：为了复用代码**
- 语法

```js
// 父类
class Father{   
} 

// 子类继承父类
class  Son extends Father {  
}       
```

- 示例

```js
class Father {
      constructor(surname) {
        this.surname= surname;
      }
      say() {
        console.log('你的姓是' + this.surname);
       }
}

class Son extends Father{  // 这样子类就继承了父类的属性和方法
    
}
var damao= new Son('刘');
damao.say();      //结果为 你的姓是刘
```

- 补充：

```js
 // 1. Son如果只是要继承父类的方法，什么都不用写
class Father {
    constructor() {

    }
    money() {
        console.log(100);

    }
}
class Son extends Father {

}
var son = new Son();
son.money();
// 2. Son如果要在父类的基础之上做扩展，就可以重写方法（重新书写）
// Son可以扩展属性，也可以扩展方法
class Father {
     constructor(x, y) {
         this.x = x;
         this.y = y;
     }
     sum() {
         console.log(this.x + this.y);

     }
 }
class Son extends Father {
    // (1)重写父类的构造函数 (主要是为了扩展属性)
    constructor(x, y, z) {
        super(x, y); //调用了父类中的构造函数
        //相当于：
        // Father(x,y);
        //相当于：
        // this.x = x; //调用父类的构造函数，让父类帮助Son添加x，y属性
        // this.y = y;
        this.z = z; // son新增的属性，需要自己处理
    };
    //（2） 自己新增的方法
    sum2() {
        console.log(this.x + this.y + this.z);
    };
    //（3）重写父类的普通方法
    sum() {
        // console.log(this.x + this.y);
        //既然要重写，肯定是要与父亲不一样，所以，改为以下需求
        //求 x  到 y 的和
    }
}
var son = new Son(1, 2, 3);
son.sum2();
son.sum();
```

- 重写：
  - 什么是重写：重新定义父类继承过来的方法 
  - 什么时候重写：子类要对父类方法进行扩展时，就可以重写方法

#### 2.2.4 super关键字

##### 1. super介绍

- super 关键字用于访问和调用对象父类上的函数。
- **可以调用父类的构造函数，也可以调用父类的普通函数** 
- super理解为父类，如果父类是Father，super等同于Father
- 语法：

```js
class Father {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    sum() {
        // console.log(this.x + this.y);//这里就不能打印结果了，需要将结果返回
        return this.x + this.y;
    }
};
class Son extends Father {
    constructor(x, y, z) {
        super(x, y); //调用了父类中的构造函数
        this.z = z; // son新增的属性，需要自己处理
    };
    // 自己新增的方法
    sum2() {
        console.log(this.x + this.y + this.z);
    };
    // 重写父类的普通方法
    sum() {
        // console.log(this.x + this.y);
        // 修改需求： x  - y 的和 
        // 扩展需求：x+y+z （扩展：是在父类基础之后进行扩展）
        var result = super.sum() + this.z;//所以利用父类的sum计算x+y，我再+z
        // Father.sum()
        console.log(result);

    }
}
var son = new Son(1, 2, 3);
// son.x,son.y,son.z
son.sum();
// super的应用场景:  在子类重写父类方法时去使用,通过super调用父类方法.
```

##### 2. super查找原则

（07-super调用父类普通函数以及继承中属性方法查找原则.avi）

super可以调用父类的构造函数，也可以调用父类的普通函数 

```js
// super 关键字调用父类普通函数
class Father {
    say() {
        return '我是爸爸';
    }
}
class Son extends Father {
    say() {
        // console.log('我是儿子');
        console.log(super.say() + '的儿子');
        // super.say() 就是调用父类中的普通函数 say()
    }
}
var son = new Son();
son.say();
```

**注意:** 

- 继承中的属性或者方法查找原则: 就近原则 
  - 继承中，如果子类对象调用一个方法，先看子类有没有这个方法，如果有就先执行子类的
  - 如果子类里面没有，就去查找父类有没有这个方法，如果有,就执行父类的这个方法

##### 3. super的位置 

（08-super必须放到子类this之前.avi）

- 如果子类想要继承父类的方法,同时在自己内部扩展自己的方法（**重写**）
- 利用super 调用父类的构造函数，super 必须在子类this之前调用
- **总结：super代码要写在重写函数的第一行**
- 例子：

```js
 // 父类有加法方法
 class Father {
   constructor(x, y) {
      this.x = x;
      this.y = y;
   }
   sum() {
      console.log(this.x + this.y);
   }
 }
 // 子类继承父类加法方法 同时 扩展减法方法
 class Son extends Father {
   //注意：这是一个固定语法：如果重写构造函数，就  必须  调用super(x,y),并且是在第一行
   constructor(x, y) {
      // 利用super 调用父类的构造函数 super 必须在子类this之前调用,放到this之后会报错
      super(x, y);
      //以下两行的代码不应该写，写也没用。因为super(x,y)调用父类构造函数，已经处理了将形参x，y赋值给this了
      this.x = x;
      this.y = y;
      //问题，如果这两行代码去掉，那么subtract中会不会报错？

  }
  subtract() {
     console.log(this.x - this.y);//不会报错，子类方法可以使用继承过来的属性x和y
  }
}
var son = new Son(5, 3);
son.subtract();
son.sum();
```

### 2.3 三个注意点

#### 1. 前两个注意点

 (09-使用类2个注意点.avi)

1. 在 ES6 中类没有变量提升，所以必须先定义类，才能通过类实例化对象. 

![](images/img2.png)

![](images/img1.png)

2. 类里面的共有属性和方法一定要加this使用.

   例子：

   ```js
   class Star {
        constructor(uname, age) {
            this.uname = uname;
            this.age = age;
            // this.sing();
            this.btn = document.querySelector('button');
            this.btn.onclick = this.sing;//必须使用this调用sing
        }
        sing() {
          	console.log(this.uname); // 必须使用this调用name
        }
    }
   var ldh = new Star('刘德华');
   //虽然sing定义的时候，没有通过this.sing定义，但是他也是属于对象的，使用必须通过 对象.方法() 调用
   ```

#### 2. this 指向问题

 (10-类里面this指向问题.avi)

- **constructor 里面的this指向实例对象**

- **方法里面的this 指向这个方法的调用者**

- 例子：

  ```js
  <body>
      <button>点击</button>
      <script>
          var that;
          var _that;
          class Star {
              constructor(uname, age) {
                  // constructor 里面的this 指向的是 创建的实例对象
                  that = this;
                  console.log(this);
  
                  this.uname = uname;
                  this.age = age;
                  // this.sing();
                  this.btn = document.querySelector('button');
                  this.btn.onclick = this.sing;
                  // 当点击了btn按钮
                  // js引擎: this.btn.onclick(); this.btn.sing();
              }
              sing() {
                  // 这个sing方法里面的this 指向的是 btn 这个按钮,因为这个按钮调用了这个函数
                  console.log(this);
  
                  console.log(that.uname); // that里面存储的是constructor里面的this
              }
              dance() {
                  // 这个dance里面的this 指向的是实例对象 ldh 因为ldh 调用了这个函数
                  _that = this;
                  console.log(this);
  
              }
          }
  
          var ldh = new Star('刘德华');
          console.log(that === ldh);//true
          ldh.dance();
          console.log(_that === ldh);//true
      </script>
  </body>
  ```

  

## 3. 面向对象版tab 栏切换

### 3.1 功能需求

1. 点击 tab栏,可以切换效果.
2. 点击 + 号, 可以添加 tab 项和内容项.
3. 点击 x 号, 可以删除当前的tab项和内容项.
4. 双击tab项文字或者内容项文字可以修改里面的文字内容

效果如下：

![](images\tab_demo.jpg)

### 3.2 案例准备

1. 获取到标题元素
2. 获取到内容元素
3. 获取到删除的小按钮 x号
4. 新建js文件,定义类,添加需要的属性方法(切换,删除,增加,修改)

5. 时刻注意this的指向问题

代码：tab.js中的代码

```js
class Tab {
    constructor(id) {
        // 获取元素
        this.main = document.querySelector(id);
        this.lis = this.main.querySelectorAll('li');
        this.sections = this.main.querySelectorAll('section');
        this.init();
    }
    init() {
        // init 初始化操作让相关的元素绑定事件
        for (var i = 0; i < this.lis.length; i++) {
            this.lis[i].index = i;
            this.lis[i].onclick = function() {
                console.log(this.index);
            };
        }
    };
    // 1. 切换功能
    toggleTab() {

    };
    // 2. 添加功能
    addTab() {

    };
    // 3. 删除功能
    removeTab(e) {

    };
    // 4. 修改功能
    editTab() {

    };

};
new Tab('#tab');
```

### 3.3 切换

代码如下：

```js
var that;//定义that
class Tab {
    constructor(id) {
        that = this;//将constructor中的this赋值给that，在事件函数中使用
        this.main = document.querySelector(id);
        this.lis = this.main.querySelectorAll('li');
        this.sections = this.main.querySelectorAll('section');
        this.init();
    }
    init() {
        for (var i = 0; i < this.lis.length; i++) {
            this.lis[i].index = i;
            this.lis[i].onclick = this.toggleTab;//给li绑定的事件定义到外边

        }
    };
    // 1. 切换功能 （这个方法是li点击事件的处理程序，所以this指向的是点击的li）
    toggleTab() {
        that.clearClass();//调用实例对象的clearClass方法
        this.className = 'liactive';
        that.sections[this.index].className = 'conactive';//让对应的section显示
    };
    // 清除所有li 和section 的类
    clearClass() {
        for (var i = 0; i < this.lis.length; i++) {
            this.lis[i].className = '';
            this.sections[i].className = '';
        }
    };

};
```



### 3.4 添加

- 上：点击添加，增加一个tab栏 

  ```js
    constructor(id) {
          that = this;
          this.main = document.querySelector(id);
          this.lis = this.main.querySelectorAll('li');
          this.sections = this.main.querySelectorAll('section');
        	//获取添加元素
          this.add = this.main.querySelector('.tabadd');
          // li的父元素
          this.ul = this.main.querySelector('.fisrstnav ul:first-child');
          this.init();
      }
      init() {
          // 给add添加点击事件
          this.add.onclick = this.addTab;
          for (var i = 0; i < this.lis.length; i++) {
              this.lis[i].index = i;
              this.lis[i].onclick = this.toggleTab;
  
          }
      };
   // 2. 添加功能
      addTab() {
          // (1) 创建li元素和section元素 
          var li = '<li class="liactive"><span>新选项卡</span><span class="iconfont icon-guanbi"></span></li>';
          // (2) 把这两个元素追加到对应的父元素里面
          that.ul.insertAdjacentHTML('beforeend', li);
      };
  ```

- 中 ： 点击添加，对应的section

  ```js
  constructor(id) {
      that = this;
      this.main = document.querySelector(id);
      this.lis = this.main.querySelectorAll('li');
      this.sections = this.main.querySelectorAll('section');
      this.add = this.main.querySelector('.tabadd');
      this.ul = this.main.querySelector('.fisrstnav ul:first-child');
      // section 父元素
      this.fsection = this.main.querySelector('.tabscon');
      this.init();
  }
  // 2. 添加功能
  addTab() {
      that.clearClass();
      // (1) 创建li元素和section元素 
      var random = Math.random();
      var li = '<li class="liactive"><span>新选项卡</span><span class="iconfont icon-guanbi"></span></li>';
      var section = '<section class="conactive">测试 ' + random + '</section>';
      // (2) 把这两个元素追加到对应的父元素里面
      that.ul.insertAdjacentHTML('beforeend', li);
      that.fsection.insertAdjacentHTML('beforeend', section);
  };
  ```

- 下：让新添加的tab也可以切换

  ```js
    constructor(id) {
          // 删掉以下两行，放到updateNode方法中
          // this.lis = this.main.querySelectorAll('li');
          // this.sections = this.main.querySelectorAll('section');
      }
      init() {
          //每次初始化都要调用更新节点方法
          this.updateNode();
          this.add.onclick = this.addTab;
          for (var i = 0; i < this.lis.length; i++) {
              this.lis[i].index = i;
              this.lis[i].onclick = this.toggleTab;
  
          }
      };
      // 因为我们动态添加元素 需要从新获取对应的元素
      updateNode() {
          this.lis = this.main.querySelectorAll('li');
          this.sections = this.main.querySelectorAll('section');
      };
  ```

  

### 3.5 删除

- 上：点击删除按钮，获取当前的索引

  ```js
   init() {
          this.updateNode();
          this.add.onclick = this.addTab;
          for (var i = 0; i < this.lis.length; i++) {
              this.lis[i].index = i;
              this.lis[i].onclick = this.toggleTab;
              //增加删除按钮的点击事件
              this.remove[i].onclick = this.removeTab;
  
          }
      };
      updateNode() {
          this.lis = this.main.querySelectorAll('li');
          this.sections = this.main.querySelectorAll('section');
          //获取删除按钮
          this.remove = this.main.querySelectorAll('.icon-guanbi');
      };
   // 3. 删除功能
  removeTab(e) {
      e.stopPropagation(); // 阻止冒泡 防止触发li 的切换点击事件
      var index = this.parentNode.index;
      console.log(index);
  
  };
  ```

- 中：点击删除当前li和section，然后让上一个tab选中

  ```js
  // 3. 删除功能
  removeTab(e) {
      e.stopPropagation(); // 阻止冒泡 防止触发li 的切换点击事件
      var index = this.parentNode.index;
      console.log(index);
      // 根据索引号删除对应的li 和section   remove()方法可以直接删除指定的元素
      that.lis[index].remove();
      that.sections[index].remove();
      that.init();
      // 当我们删除了选中状态的这个li 的时候, 让它的前一个li 处于选定状态
      index--;
      // 手动调用我们的点击事件  不需要鼠标触发
      that.lis[index] && that.lis[index].click();
  
  };
  ```

- 下：当我们删除的不是选中状态的li 的时候,原来的选中状态li保持不变

  ```js
  removeTab(e) {
      e.stopPropagation();
      var index = this.parentNode.index;
      console.log(index);
      that.lis[index].remove();
      that.sections[index].remove();
      that.init();
      // 当我们删除的不是选中状态的li 的时候,原来的选中状态li保持不变
      if (document.querySelector('.liactive')) return;
      index--;
      that.lis[index] && that.lis[index].click();
  
  };
  ```

  

### 3.6 编辑

- 上：双击tab文字，将span内添加文本框

  ```js
  updateNode() {
      this.lis = this.main.querySelectorAll('li');
      this.sections = this.main.querySelectorAll('section');
      this.remove = this.main.querySelectorAll('.icon-guanbi');
      //找到文字，用于添加双击事件
      this.spans = this.main.querySelectorAll('.fisrstnav li span:first-child');
  };
  init() {
      this.updateNode();
      this.add.onclick = this.addTab;
      for (var i = 0; i < this.lis.length; i++) {
          this.lis[i].index = i;
          this.lis[i].onclick = this.toggleTab;
          this.remove[i].onclick = this.removeTab;
          //给span添加双击事件
          this.spans[i].ondblclick = this.editTab;
      }
      };
     // 4. 修改功能
  editTab() {
      // 双击禁止选定文字
      window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
      this.innerHTML = '<input type="text" />';
  };
  ```

- 中：双击之后，将span原本内容显示到text中，并让text处理选中状态。离开时，让span文字等于text文字。

  ```js
  // 4. 修改功能
  editTab() {
      var str = this.innerHTML;
      // 双击禁止选定文字
      window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
      // alert(11);
      this.innerHTML = '<input type="text" />';
      var input = this.children[0];
      input.value = str;
      input.select(); // 文本框里面的文字处于选定状态
      // 当我们离开文本框就把文本框里面的值给span 
      input.onblur = function() {
          this.parentNode.innerHTML = this.value;
      };
  };
  ```

- 下：修改文本内容后，按回车触发blur事件。section添加双击事件，可以编辑。

  ```js
  editTab() {
      var str = this.innerHTML;
      window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
      // alert(11);
      this.innerHTML = '<input type="text" />';
      var input = this.children[0];
      input.value = str;
      input.select(); 
      input.onblur = function() {
          this.parentNode.innerHTML = this.value;
      };
      // 按下回车也可以把文本框里面的值给span
      input.onkeyup = function(e) {
          if (e.keyCode === 13) {
              // 手动调用表单失去焦点事件  不需要鼠标离开操作
              this.blur();
          }
      }
  };
  init() {
      this.updateNode();
      this.add.onclick = this.addTab;
      for (var i = 0; i < this.lis.length; i++) {
          this.lis[i].index = i;
          this.lis[i].onclick = this.toggleTab;
          this.remove[i].onclick = this.removeTab;
          this.spans[i].ondblclick = this.editTab;
          //section添加双击事件，可以编辑
          this.sections[i].ondblclick = this.editTab;
  
      }
  };
  ```

  

