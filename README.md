## 需要使用外层容器包裹并设置宽高

## 使用 注意： 需要关掉本地的mock服务， 不然图片转化会报错 
```
组件内使用
import { VueCropper }  from 'vue-cropper' 
components: {
  VueCropper,
},

main.js里面使用
import VueCropper from 'vue-cropper' 

Vue.use(VueCropper)

cdn方式使用
<script src="//cdn.jsdelivr.net/npm/vue-cropper@0.4.9/dist/index.js"></script>
Vue.use(window['vue-cropper'].default)
nuxt 使用方式
if(process.browser) {
  vueCropper = require('vue-cropper')
  Vue.use(vueCropper.default)
}

```

``` html
<vueCropper
  ref="cropper"
  :img="option.img"
  :outputSize="option.size"
  :outputType="option.outputType"
></vueCropper>
```


# vue-cropper

#### 安装 
```
npm install vue-cropper

yarn add vue-cropper
```





### 如果你没有使用npm
[在线例子](https://codepen.io/xyxiao001/pen/wxwKGz)

### 服务器渲染 nuxt 解决方案 设置为ssr: false
```
module.exports = {
  ...
  build: {
    vendor: [
      'vue-cropper
    ...
    plugins: [
      { src: '~/plugins/vue-cropper', ssr: false }
    ]
  }
}
```

###  目前还不知道什么原因项目里面开启mock 会导致file报错, 建议使用时 关掉mock


<table style="text-align: center">
  <thead>
    <tr>
        <td>名称</td>
        <td>功能</td>
        <td>默认值</td>
        <td>可选值</td>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td>img</td>
        <td>裁剪图片的地址</td>
        <td>空</td>
        <td>url 地址 || base64 || blob</td>
    </tr>
    <tr>
        <td>outputSize</td>
        <td>裁剪生成图片的质量</td>
        <td>1</td>
        <td>0.1 - 1</td>
    </tr>
    <tr>
        <td>outputType</td>
        <td>裁剪生成图片的格式</td>
        <td>jpg (jpg 需要传入jpeg)</td>
        <td>jpeg || png || webp</td>
    </tr>
    <tr>
        <td>info</td>
        <td>裁剪框的大小信息</td>
        <td>true</td>
        <td>true || false</td>
    </tr>
    <tr>
        <td>canScale</td>
        <td>图片是否允许滚轮缩放</td>
        <td>true</td>
        <td>true || false</td>
    </tr>
    <tr>
        <td>autoCrop</td>
        <td>是否默认生成截图框</td>
        <td>false</td>
        <td>true || false</td>
    </tr>
    <tr>
        <td>autoCropWidth</td>
        <td>默认生成截图框宽度</td>
        <td>容器的80%</td>
        <td>0~max</td>
    </tr>
    <tr>
        <td>autoCropHeight</td>
        <td>默认生成截图框高度</td>
        <td>容器的80%</td>
        <td>0~max</td>
    </tr>
    <tr>
        <td>fixed</td>
        <td>是否开启截图框宽高固定比例</td>
        <td>true</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>fixedNumber</td>
        <td>截图框的宽高比例</td>
        <td>[1, 1]</td>
        <td>[宽度, 高度]</td>
    </tr>
    <tr>
        <td>full</td>
        <td>是否输出原图比例的截图</td>
        <td>false</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>fixedBox</td>
        <td>固定截图框大小 不允许改变</td>
        <td>false</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>canMove</td>
        <td>上传图片是否可以移动</td>
        <td>true</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>canMoveBox</td>
        <td>截图框能否拖动</td>
        <td>true</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>original</td>
        <td>上传图片按照原始比例渲染</td>
        <td>false</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>centerBox</td>
        <td>截图框是否被限制在图片里面</td>
        <td>false</td>
        <td>true | false</td>
    </tr>
	<tr>
        <td>high</td>
        <td>是否按照设备的dpr 输出等比例图片</td>
        <td>true</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>infoTrue</td>
        <td>true 为展示真实输出图片宽高  false 展示看到的截图框宽高</td>
        <td>false</td>
        <td>true | false</td>
    </tr>
    <tr>
        <td>maxImgSize</td>
        <td>限制图片最大宽度和高度</td>
        <td>2000</td>
        <td>0-max</td>
    </tr>
    <tr>
        <td>enlarge</td>
        <td>图片根据截图框输出比例倍数</td>
        <td>1</td>
        <td>0-max(建议不要太大不然会卡死的呢)</td>
    </tr>
    <tr>
        <td>mode</td>
        <td>图片默认渲染方式</td>
        <td>contain</td>
        <td>contain , cover, 100px, 100% auto</td>
    </tr>
  </tbody>
</table>


### 内置方法  通过this.$refs.cropper 调用
##### this.$refs.cropper.startCrop()  开始截图
##### this.$refs.cropper.stopCrop()  停止截图
##### this.$refs.cropper.clearCrop()  清除截图
##### this.$refs.cropper.changeScale()  修改图片大小 正数为变大 负数变小
##### this.$refs.cropper.getImgAxis() 获取图片基于容器的坐标点
##### this.$refs.cropper.getCropAxis() 获取截图框基于容器的坐标点
##### this.$refs.cropper.goAutoCrop 自动生成截图框函数
##### this.$refs.cropper.rotateRight() 向右边旋转90度
##### this.$refs.cropper.rotateLeft() 向左边旋转90度

####  图片加载的回调 imgLoad  返回结果success,  error

####  获取截图信息
this.$refs.cropper.cropW  截图框宽度

this.$refs.cropper.cropH 截图框高度
``` js
// 获取截图的base64 数据
this.$refs.cropper.getCropData((data) => {
  // do something
  console.log(data)  
})

// 获取截图的blob数据
this.$refs.cropper.getCropBlob((data) => {
  // do something
  console.log(data)  
})

### Description of the default rendering mode of the image
Image layout mode mode achieves the same effect as css background
Contain Centered layout Default does not scale Ensure the image is inside the container mode: 'contain'
Cover stretch layout fill the entire container mode: 'cover'
If only one value is given, this value will be used as the width value and the height value will be set to auto. mode: '50px'
If two values are given, the first one will be the width value and the second will be the height value. mode: '50px 60px'

### 预览
``` html
@realTime="realTime"
// Real time preview function
realTime(data) {
  var previews = data;
  var h = 0.5;
  var w = 0.2;

  this.previewStyle1 = {
    width: previews.w + "px",
    height: previews.h + "px",
    overflow: "hidden",
    margin: "0",
    zoom: h
  };

  this.previewStyle2 = {
    width: previews.w + "px",
    height: previews.h + "px",
    overflow: "hidden",
    margin: "0",
    zoom: w
  };

  固定为100宽度
  this.previewStyle3 = {
    width: previews.w + "px",
    height: previews.h + "px",
    overflow: "hidden",
    margin: "0",
    zoom: 100 / preview.w
  };

  固定为100高度
  this.previewStyle4 = {
    width: previews.w + "px",
    height: previews.h + "px",
    overflow: "hidden",
    margin: "0",
    zoom: 100 / preview.h
  };
  this.previews = data;
},


<div class="show-preview" :style="{'width': previews.w + 'px', 'height': previews.h + 'px',  'overflow': 'hidden',
    'margin': '5px'}">
  <div :style="previews.div">
    <img :src="option.img" :style="previews.img">
  </div>
</div>
<p>中等大小</p>
<div :style="previewStyle1"> 
  <div :style="previews.div">
    <img :src="previews.url" :style="previews.img">
  </div>
</div>

<p>迷你大小</p>
<div :style="previewStyle2"> 
  <div :style="previews.div">
    <img :src="previews.url" :style="previews.img">
  </div>
</div>
=
```

#### 图片移动回调函数 @imgMoving
```
data type
{
   moving: true, // moving 是否在移动
   axis: {
    x1: 1, // 左上角
	 x2: 1，// 右上角
	 y1: 1，// 左下角
	 y2: 1 // 右下角
   }
 }
```

#### 截图框移动回调函数 @cropMoving
```
data type
{
   moving: true, // moving 是否在移动
   axis: {
    x1: 1, // 左上角
	 x2: 1，// 右上角
	 y1: 1，// 左下角
	 y2: 1 // 右下角
   }
 }
```


## 更新日志


### 0.49
修复滚轮默认事件问题
修复html静态文件引入事件触发问题

### 0.48
修复mode 属性 contain 和cover的显示bug问题

修复ios 下面base64图片跨域显示问题


### 0.47
修复第一次不触发预览的问题
新增加图片渲染mode功能

### 0.46
修复图片旋转bug
修复显示的一些bug

### 0.45 
添加倍数使用 enlarge
可以输出裁剪框等比例图片；


### 0.44
修复引入方式的问题
```
组件内使用
import { VueCropper }  from vue-cropper 
components: {
  VueCropper,
},

main.js里面使用
import VueCropper from vue-cropper 

Vue.use(vueCropper)

cdn方式使用
<script src="vuecropper.js"></script>
Vue.use(window['vue-cropper'])
```

