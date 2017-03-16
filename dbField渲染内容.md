# 啊
当json数据不是数组类型需要循环渲染输出html代码时，
```js
res = {
    "status": 1,
    "message": null,
    "code": null,
    "data": {
        "course": {
            "name": "name",
            "title": "title",
            "teacherName": "teacherName",
            "avatar": "avatar.jpg",
            "teacherTitle": "teacherTitle",
            "during": 20,
            "intro": "intro",
            "joinNum": 5,
            "likeNum": 1,
            "gmtCreate": 1489029136000,
            "categoryName": categoryName,
            "cover": "cover.jpg",
            "discussNum": 16
        },
        "avatarUrls": {
            "status": 1,
            "message": null,
            "code": null,
            "data": [
                "1.png",
                "2.jpg",
                "3.jpg",
                "4.jpg",
                "5.jpg"
            ]
        }
    }
}
```
# 实操

## html
```
在标签添加'dbField'属性
<p dbField="status"></p> ==> <p dbField="message">1</p>
<p dbField="data.course.name"></p>  ==> <p dbField="data.course.name">name</p>
<img dbField="data.avatarUrls.data.1"/> ==> <img dbField="data.avatarUrls.data.1" src="1.png"/>
```
## JS
```js
var target = $coverPageEl,
    dbFieldLists = $('[dbField]', target);
for (var i = 0, len = dbFieldLists.length; i < len; i++) {

    (function($self) {
        var targetBdfield = $self.attr('dbField'),
            dbArrary = targetBdfield.split('.'),
            dbObj = data;
        for (var j = 0, dbLen = dbArrary.length; j < dbLen; j++) {
            if (dbObj[dbArrary[j]] !== undefined) {
                var objName = dbArrary[j];
                dbObj = dbObj[objName];

                // console.log(dbObj)
            } else {
                dbObj = 0;
            }
        }
        if ($self[0].tagName == 'IMG') {
            $self.attr('src', dbObj + $self.data('style'));
        } else {
            $self.html(dbObj);
        }

    })($(dbFieldLists[i]));
}
```
