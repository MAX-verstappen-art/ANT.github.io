# Bugku Web 你必须让他停下
## 题目描述
页面会自动高频刷新，提示`Stop at panda ! u will get flag`，页面刷新速度过快，无法肉眼观察flag。

## 考点
JS自动刷新、HTTP原始响应包抓取

## 解题过程
1. 访问页面，查看源码发现存在JS定时重载代码：
```javascript
function myrefresh(){
    window.location.reload();
}
setTimeout('myrefresh()',500);
