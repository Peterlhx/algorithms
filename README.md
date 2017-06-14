# algorithms
收集一些常见的算法题

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
