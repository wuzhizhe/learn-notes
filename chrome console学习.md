= 学习chrome console =

   这里记录从Google开发者网站的官方文档中看到的chrome console的用法。

== 1. 综述 ==
  
  1.1 chrome默认重复数据不全部在console中显示，而是用数字表示重复次数，这个可以在console的setting中设置使用时间戳展示，这样就没有重复数据了。

  1.2 清除console界面的所有数据，方法有：clear(), console.clear(),鼠标右键清除， ctrl+l，最后一个肯定是最方便了，不用打字不用鼠标并且全系统通用。

  1.3 保存console历史纪录，鼠标右键save as。

  1.4 选择执行console的上下文，主要用来处理对于不同iframe的情况，当然可以支持chrome浏览器下不同的extension、app。

  1.5 filter过滤console output的结果，有all errors warnings info logs等等，可以直接在右边选择。高级的用法支持正则表达式来筛选过滤结果。

== 2. 输出log到console ==

  1.1 console.log，这个就是最常用的方法了，我几乎没用过什么别的方法，将你要展示的信息输出到log上。

  1.2 对log信息进行分组，如果你觉得输出的log有必要分组可以用console.group()方法进行分组输出，在分组结束时用console.groupEnd()结束当前分组。分组支持多级嵌套，嵌套中药完整的开始结束相关分组。

  1.3 错误提示。 console.error()；

  1.4 警告其实。 console.warn();

  1.5 断言提示。 console.assert()
  
  1.6 **字符串替换以及格式化功能** 
   我觉得这个功能还是很强大的，一般的js不用这些功能吧，但是chrome支持，这个就比较给力了。
   | Specifier | Output |
   | ------ | ------ |
   | %s | Formats the value as a string |
   | %i or %d | Formats the value as an integer |
   | %f | Formats the value as a floating point value |
   | %o | Formats the value as an expandable DOM element. As seen in the Elements panel |
   | %O | Formats the value as an expandable JavaScript object |
   | %c | Applies CSS style rules to the output string as specified by the second parameter |

== 3. 数据对比 ==
  
  数据对比使用console.table()方法，支持两个参数，第一个是数组，数组中的每个参数可以是数据，也可以是JSON数据。
  第二个参数也是个数组，设置要打印的property名称。具体的代码例子如下：

  ```javascript
    
console.table([{a:1, b:2, c:3}, {a:"foo", b:false, c:undefined}]);
console.table([[1,2,3], [2,3,4]]);

function Person(firstName, lastName, age) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.age = age;
}

var family = {};
family.mother = new Person("Susan", "Doyle", 32);
family.father = new Person("John", "Doyle", 33);
family.daughter = new Person("Lily", "Doyle", 5);
family.son = new Person("Mike", "Doyle", 8);

console.table(family, ["firstName", "lastName", "age"]);

  ```
