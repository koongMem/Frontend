<h3>方法一：</h3>
通过import直接引入，直接调用data即可获取json文件的内容。

```
import data from 'static/h5Static.json'
```
该方法比较直接，但是打包以后发现变更JSON文件，结果渲染的页面还是与最初打包JSON文件渲染出来的页面一样，并不能达到我想要的结果，因此尝试了方法二。


<h3>方法二：</h3>
通过axios请求的方式，可参考上一篇博客axios的封装<br/>
1.在http.js中添加一个请求方法

```
export const $getJson = function (method) {
  return new Promise((resolve, reject) => {
    axios({
      method: 'get',
      url: method,
      dataType: "json",
      crossDomain: true,
      cache: false
    }).then(res => {
      resolve(res)
    }).catch(error => {
      reject(error)
    })
  })
```
2.接口的封装文件中引入$getJson请求方式

```
import{$get,$post,$getJson}from '../http';

//获取JSON数据
const getH5StaticJson = data => {
  return $getJson('static/h5Static.json',data)
}
```
3.在组件中使用

```
this.$api.user.getH5StaticJson({}).then(res => {
     consloe.log(res)
});
```

感恩： https://www.cnblogs.com/yy136/p/9977864.html
