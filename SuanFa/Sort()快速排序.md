# 用sort()方法实现数字排序
### sort用法

sort根据ascall码排序规则比较，在比之前会把所传参数字符串化，然后从左到右进行比较，优先级为 `数字>大写字母>小写字母>汉字`

## 题目描述
`对一个数组内数字进行排序，数组全是整数数字`
```js
function numbers(nums){
    let SortNum = nums.sort((a,b)=>(a-b));
    return SortNum;
        }
```
sort进行排序会两两比较，
* 若a-b>0,则将a放在b后面
* a-b<0,将a放在b前面
* a-b=0，不会进行交换