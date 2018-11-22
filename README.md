# weexQuestion
项目中遇到的weex，weex的UI相关的问题
***

|Author|wangxi|
|---|---
|E-mail|18309292050@163.com


***
## 目录
* weex简介(#weex简介)
* [一些项目中遇到的问题](#一些项目中遇到的问题)
    * px实现响应式
    * 样式改变
    * textarea中的oninput
    * weex-ui中步进器的使用
    * 多个class并写三元判断
    * weex不支持公共样式
    * weex中手机端样式显示不出原因
    * weex中的判断问题
* weex中默认布局flex

### weex简介
```
1.h5页面，安卓，ios共用一套代码
2.h5的写法创建页面，安卓和ios调取页面的链接
3.h5调用原生的组件，安卓和ios负责拓展功能

weex的优势
1.调用的原生组件所以用户体验度好
2.h5开发速度快，节约成本

weex的劣势
1.文档不健全，学习难度大
2.坑点较多
```
### 一些项目中遇到的问题

#### 1. px实现响应式
   **每一个text标签必须单独设置font-size**，不能按照之前的逻辑父级设了子级不设
#### 2.样式改变
   -**如果要实现改变样式需要写成内部样式然后通过改变class来实现**，如果写了行内样式然后通过if来判断使用不同标签来达到切换样式是行不通的，真机上会出现复用情况，同理写了class然后用行内样式覆盖也是一样出现复用问题
   **还可以通过提供的animation模块动画时间调为0完成样式的覆盖**
#### 3.textarea中oninput
   **真机使用这个事件无法获取到框内的值并且里面没有value属性**
   **解决方案：**
   ```javascript
   //1.data中设置一个对象
   textareaObj:{},
   //2.加载数据时给对象中添加对应个数的属性
   for(let i= 0; i < this.lists.length; ++i){
      let textareaValue={};
      let store_id =this.lists[i].store_id;
      textareaValue[store_id] ='';
      Object.assign(this.textareaObj,textareaValue);
   }
   //3.查找对应属性的值并实现实时绑定
   v-model="textareaObj[item.store_id]"
   ```
