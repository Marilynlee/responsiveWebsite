# Notes
## 响应式布局
响应式时布局是指：弹性布局、弹性图片、媒体查询.根据浏览器的尺寸进行自由的变化和布局。

## 项目结构
robots.txt 解释网站可抓取的信息以及不可以抓取的内容
humans.txt 保存网站的开发人员、团队等信息

## css尺寸
+ px是固定单位，不回根据响应布局改变大小1px=1像素
+ em相对单位，参照父元素的font-size大小，具有继承特性。当未设置font-size时，浏览器会默认1em=16px
缺点：易于混乱
+ rem相对单位，参照根元素html的font-size大小，参照物固定易于计算.当未设置font-size时，浏览器会默认1rem=16px
缺点：易于混乱
+ media作为最高级的媒体查询与html级别相同，并不参考html的尺寸,遵循浏览器默认值1rem=16px
``` 
@media only screen and (max-width: 50em) {} 
```
+ 默认html的font-size=16px 若设置62.5%即为10px=16px*62.5%，为了rem和px的相互转化即1rem=10px,便于计算
 ```
  html {    font-size: 62.5%;  }	
 ```
+ 中文版chrome设置3rem行高=36px，因为中文chrome默认设置最小文字大小为12px

## 响应式图片
根据设备大小图片的布局和排版不同，且加载不同尺寸的图片。
实现方式：
1. js/服务端：  
通过js查询设备尺寸，加载不同尺寸的图片
把屏幕尺寸信息写入cookie，提交服务端，返回不同尺寸的图片
1. srcset：  
声明多组图片路径和尺寸，支持srcset的浏览器会综合根据页面大小、网速、分辨率、dpr等进行选择  
但是只设置srcset图片加载会混乱，小屏幕下也会加载大图 
 ```html
<img src='img480.png' srcset='img480.png 480w, img960.png 960w, img1600.png 1600w'/>
 ```
1. srcset+sizes：  
sizes如果不设置默认为100vw（100%视口宽度），总是根据视口宽度进行图片选择，而忽略图片和其盒子实际尺寸
sizes可设置多组媒体查询条件和图片尺寸，根据媒体查询条件进行图片选择
 ``` html
<img src="img.png"srcset="img480.png 480w, img960.png 960w, img1600.png 1600w"
sizes="(min-width:800px) calc(100vw - 30em), 100vw"/> 
 ```
1. picture：  
picture可以加强对图片的控制权，可根据尺寸大小加载不同效果图，比如小屏幕加载裁切版本图片
可以根据媒体查询、图片格式等进行图片的选择

``` HTML
<picture>
  <source srcset="ad001-l.png" media="(min-width:50em)">
  <source srcset="ad001-m.png" media="(min-width:30em)">
  <source srcset="ad001-m.png" media="(orientation:landscape)">
  <source type="image/svg+xml" srcset="ad001.svg 30em">
  <source type="image/webp" srcset="ad001-m.webp 30em,ad001-l.webp 50em,">
  <img src="ad001.png">
</picture> 
 ```
1. svg：  
矢量图形是最完美的解决方案，相比srcset和picture兼容性好，但是图片过大不适合svg，可用于一些小的图标







