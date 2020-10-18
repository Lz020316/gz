## 技术栈

> 1、jquery.js
>
> 2、swiper
>
> 3、animate库
>
> 4、less
>
> 5、wow

## 功能的实现

### 附加导航和 滚动监听的实现

##### 附加导航

当滚动条滚动时
  如果 winTop >= target.offset().top 时
    给target加固定定位
  如果 winTop > target.next().offset().top - target.height() 时
    去掉target的定位
##### 滚动监听

```javascript
function scrollMonitor(winTop, Sel, select) {
  if (winTop >= getTop(Sel) || winTop <= getBottom(Sel))
    $(select).addClass("on").siblings().removeClass("on");
}
```
### wow插件基本的使用

需要配合animate库的使用

```html
<div class="wow fadeInLeft animated"></div>
```
```javascript
if (!/msie [6|7|8|9]/i.test(navigator.userAgent)) {
  new WOW().init();
}
```
### less 编译

可以是使用koala.exe软件编译 或者使用 grunt
vscode里面也有插件可以编译

### 3d汽车旋转

```javascript
function renderCar(imgAddress) {
        $(".imgBox").html("");
        for (let i = 1; i <= 35; i++) {
          const img = `<img src="imgs/index/${imgAddress}/pic_${i}.png" draggable="false" class="hide">`;
          // $("img").addClass("hide");
          $(".imgBox").append(img);
        }

        const $imgs = $(".imgBox img");
        $imgs.eq(0).show();
        let lastIndex = 0; // 当前横坐标坐标
        let startX = 0; // 记录鼠标点下时的横坐标
        let index = 0; //  记录鼠标移动的坐标距离
        let prevImg = null;
        let boo = false;
        $(".imgBox").mousedown(function (ev) {
          if (!boo) {
            boo = true;
            $("#img0").remove();
            startX = ev.clientX;  // 鼠标第一次按下的x值
          }
        });
        $(document).mousemove(function (ev) {
          if (boo) {
            let x = ev.clientX; // 移动时的x值
            let dis = x - startX;  // 按下和移动时值之间的距离
            if (dis >= 0) {
              index = (Math.floor(dis / 20) + lastIndex) % 35;
            } else {
              index = (35 + Math.floor(dis / 20) + lastIndex) % 35;
            }
            if (prevImg) prevImg.addClass("hide");
            // console.log(index);
            $imgs
              .eq(index + 1)
              .show()
              .siblings()
              .hide();
            prevImg = $imgs.eq(index);
          }
        });

        $(document).mouseup(() => {
          if (boo) {
            boo = false;
          }
        });
      }
```
