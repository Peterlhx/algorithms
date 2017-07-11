# algorithms
收集一些常见的算法题

## 1到9组合计算等于100
> 将1，2，3，4，5，6，7，8，9通过''、'+'、'-'组合计算等于100，数字顺序不可改变，例如：1+2+34-5+67-8+9 = 100

采用递归实现：
```js
const symbols = ['', '+', '-'];
const nums = [1, 2, 3, 4, 5, 6, 7, 8, 9];

var exp = '';
function calToHundred (nums, index, symbols) {
  if(index === 8) {
    exp += '9'
    // 计算是否等于100
    if (eval(exp) === 100) {
      console.log(exp + ' = 100');
    }
    // 回退上一步
    exp = exp.substr(0, exp.length - 1);
    return;
  }

  exp += nums[index];
  // 依次执行''、'+'、'-'的递归
  for (let i = 0, len = symbols.length; i < len; i++) {
    if (i > 1) {
      exp = exp.substr(0, exp.length - 1);
    }
    exp += symbols[i];
    calToHundred(nums, index + 1, symbols);
  }
  // 当执行'+'、'-'递归后，需要去除尾部的'+'、'-'
  exp = exp.substr(0, exp.length - (symbols.length - 1));
}

// 代码开始执行
calToHundred (nums, 0, symbols);
```
上述代码的主要思想是：将计算表达式设置为字符串，然后通过递归，穷举所有可能的情况，通过eval()将表达式字符串编译执行，输出等于100的表达式。


## 快速排序
> 快速排序是最常见的一种排序算法，其核心算法就是找一个基准值，根据这个基准值将一个数组分成两个子数组，逐渐递归

```js
var quickSort = function (arr) {
  var len = arr.length, 
    pivotIndex = Math.floor(len / 2), /* 找中间的一个数只是为了方便理解，基准值可以是数组中任意一个数 */
    pivot = arr.splice(pivotIndex, 1)[0];
  var left = [], right = [];
  if (len <= 1) {
    return;
  }
  arr.forEach(function (item) {
    if (item < pivot) {
      left.push(item)
    } else {
      right.push(item)
    }
  })

  return quickSort(left).concat([pivot], quickSort(right));
}
```
推荐一篇博文[http://louiszhai.github.io/2016/12/23/sort/](http://louiszhai.github.io/2016/12/23/sort/) ，里面讲了各种排序算法，还配有排序动画，非常不错


## 二叉树遍历
> 今天复习下二叉树的遍历，一听到二叉树相关的，可能有些小伙伴会觉得很复杂，但是二叉树遍历可能要让你们失望了，因为它很简单，实现二叉树遍历只要四五代码

二叉树遍历有先序遍历，中序遍历，后序遍历三种：

1.先序遍历：首先访问根结点，然后遍历左子树，最后遍历右子树。简记根-左-右；

2.中序遍历：首先遍历左子树，然后访问根结点，最后遍历右子树。简记左-根-右；

3.后序遍历：首先遍历左子树，然后遍历右子树，最后访问根结点。简记左-右-根。 

代码
代码实现：
```js
/*先序遍历*/
function preOrder(node){
  if(node){
    console.log(node.show()+' ');   /*将该语句与下方两条语句进行位置调换，即可实现不同的遍历顺序*/
    arguments.callee(node.left);
    arguments.callee(node.right);
  }
}
```

