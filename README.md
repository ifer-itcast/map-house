## 00_初始化地图

[文档链接](http://lbsyun.baidu.com/index.php?title=jspopular3.0/guide/helloworld)

## 01_根据定位展示当前城市

`就是根据地址解析出poin，然后调用 map.centerAndZoom(point, 11) 即可`

1. 获取当前定位城市

```javascript
const pos = { "label": "上海", "value": "AREA|dbf46d32-7e76-1196" };
```

2. 使用地址解析器解析当前城市坐标，[链接](http://lbsyun.baidu.com/index.php?title=jspopular3.0/guide/geocoding)

3. 调用 centerAndZoom() 方法在地图中展示当前城市，并设置缩放级别为 11

4. 在地图中展示该城市，并添加比例尺和平移缩放控件，[文档](http://lbsyun.baidu.com/index.php?title=jspopular3.0/guide/widget)

```javascript
// 平移缩放
map.addControl(new BMap.NavigationControl());
// 比例尺
map.addControl(new BMap.ScaleControl());
```

## 02_创建文本覆盖物

[文档](http://lbsyun.baidu.com/jsdemo.htm#c1_14)

1. 创建 Label 实例对象

2. 调用 setStyle() 方法设置样式

3. 在 map 对象上调用 addOverlay() 方法，将文本覆盖物添加到地图中

```javascript
const opts = {
    position: point,
    offset: new BMap.Size(30, -30)
}
const label = new BMap.Label("欢迎使用百度地图，这是一个简单的文本标注哦~", opts);  // 创建文本标注对象
label.setStyle({
    color: "red",
});
map.addOverlay(label);
```

## 03_创建房源覆盖物，[文档](http://lbsyun.baidu.com/cms/jsapi/reference/jsapi_webgl_1_0.html#a3b8)

1. 调用 Label 的 setContent 方法，传入 html 结构，修改 HTML 的内容样式;注意：调用了 setContent 那么里面文本的内容就失效了

```javascript
label.setContent(`
    <div class="bubble">
        <p class="name">浦东</p>
        <p>99套</p>
    </div>
`);
```

2. 调用 setStyle 方法修改覆盖物样式

3. 给覆盖物添加点击事件

```javascript
label.addEventListener('click', function() {
    console.log('x');
});
```

4. 在 map 对象上调用 addOverlay() 方法，将房源覆盖物 label 添加到地图中

## 功能分析

1. 获取房源数据，渲染覆盖物

2. 点击覆盖物，放大地图，获取数据，渲染下一级覆盖物（重复步骤1）

3. 区、镇覆盖物的点击事件中，清除现有的覆盖物，获取下一级数据，创建新的覆盖物

4. 小区：不清除覆盖物，移动地图，展示该小区下的房源信息

## 04_渲染所有区的覆盖物

1. 发送请求获取房源数据

2. 遍历数据，创建覆盖物，给每一个覆盖物添加唯一标识（后面要用）

3. 给覆盖物添加点击事件

4. 在单击事件中，获取到当前单击项的唯一标识

5. 放大地图（级别为13），调用 clearOverlays() 方法清除当前覆盖物

## 05_renderOverlays

## 06_createOverlays

## 07_createCircle

## 08_createRect


