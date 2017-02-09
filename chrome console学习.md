##学习chrome console

   这里记录从Google开发者网站的官方文档中看到的chrome console的用法。

###1. 综述
  
  1.1 chrome默认重复数据不全部在console中显示，而是用数字表示重复次数，这个可以在console的setting中设置使用时间戳展示，这样就没有重复数据了。

  1.2 清除console界面的所有数据，方法有：clear(), console.clear(),鼠标右键清除， ctrl+l，最后一个肯定是最方便了，不用打字不用鼠标并且全系统通用。

  1.3 保存console历史纪录，鼠标右键save as。

  1.4 选择执行console的上下文，主要用来处理对于不同iframe的情况，当然可以支持chrome浏览器下不同的extension、app。

  1.5 filter过滤console output的结果，有all errors warnings info logs等等，可以直接在右边选择。高级的用法支持正则表达式来筛选过滤结果。

###2. 输出log到console

  2.1 console.log，这个就是最常用的方法了，我几乎没用过什么别的方法，将你要展示的信息输出到log上。

  2.2 对log信息进行分组，如果你觉得输出的log有必要分组可以用console.group()方法进行分组输出，在分组结束时用console.groupEnd()结束当前分组。分组支持多级嵌套，嵌套中药完整的开始结束相关分组。

  2.3 错误提示。 console.error()；

  2.4 警告提示。 console.warn();

  2.5 断言提示。 console.assert()

  2.6 **字符串替换以及格式化功能** 
   我觉得这个功能还是很强大的，一般的js不用这些功能吧，但是chrome支持，这个就比较给力了。
   | Specifier | Output |
   | ------ | ------ |
   | %s | Formats the value as a string |
   | %i or %d | Formats the value as an integer |
   | %f | Formats the value as a floating point value |
   | %o | Formats the value as an expandable DOM element. As seen in the Elements panel |
   | %O | Formats the value as an expandable JavaScript object |
   | %c | Applies CSS style rules to the output string as specified by the second parameter |

###3. 数据对比
  
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

###4. 计时与计数
  
  4.1 计时
  用console.time()开始计时，用console.timeEnd()结束计时。计时函数支持字符串参数来说明是为什么计时的。

  4.2 计数
  用console.count()方法进行计数，所有经过count函数的内容，只要与前面的内容相同就会计数加一。

###5. error and exception
  
  5.1 throw Exception
  javascript可以直接throw exception，例如throw 'exception happened!'

  5.2 stack trace 
  event中的e.stack以及 console.trace()可以追踪函数的调用以及stack产生的顺序。

  5.3 onerror函数处理错误
  这里的onerror有window上的global级别的，也可以设置到具体的element上，下面是MDN上的一段代码示例：

  ```javascript

  window.onerror = function (msg, url, lineNo, columnNo, error) {
      var string = msg.toLowerCase();
      var substring = "script error";
      if (string.indexOf(substring) > -1){
          alert('Script Error: See Browser Console for Detail');
      } else {
          var message = [
              'Message: ' + msg,
              'URL: ' + url,
              'Line: ' + lineNo,
              'Column: ' + columnNo,
              'Error object: ' + JSON.stringify(error)
          ].join(' - ');

          alert(message);
      }

      return false;
  };

  ```

  具体的详细说明见MDN官网[GlobalEventHandlers.onerror](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onerror)

###6. 其余常用consle api
  
  6.1 console.dir()
  这个方法可以将js对象或者dom元素的对象展示出来，dom元素的展示包含其所有的属性方法

  6.2 console.dirxml()
  这个方法也可以将js对象或者dom元素的对象展示出来，但是不同的是在展示dom元素对象的时候只会展示其子元素相关的dom element信息，不会像dir()那样展示所有的属性。

  6.3 console.info()
  这个方法跟console.log()的展现几乎是一样的，但是它的前面有个蓝色i的小图标。

  6.4 console.profile()
  与profileEnd()搭配，目前完全不知道是做什么的，后期用了再补充吧。

###7. select/inspect Elements

  7.1 select elements
  这个可以用类似jQuery的$符，不过在chrome的console中的$与jquery的$还是有区别的，具体如下：
  $() 指的是document.querySelector(), $$()指的是document.querySelectorAll(),$x()支持根据xpath选择相应的element，xpath之前没有了解过，w3school上的相关信息[XPath Syntax](http://www.w3schools.com/xml/xpath_syntax.asp)

  7.2 insepect Dom Elements
  inspect($('/html/body'))

  7.3 recent selected elements and objects
  $0 $1 $2 $3 $4 时间顺序由近到远

###8. monitor events 事件监听

  8.1  monitorEvents
  使用monitorEvents()方法来监听，使用unmonitorEvents()停止监听，例子：
  ```javascript

  monitorEvents(document.body, "click");
  unmonitorEvents(document.body);

  ```

  8.2 getEventListeners()
  获取某个Dom元素上的所有的事件，使用方法getEventListeners(document.body)

  8.3 在panel上展开针对某个DOM Element的event