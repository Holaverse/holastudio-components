自定义组件实现虚拟摇杆(joystick)
----------------------------------------

* 1.在场景中放一个按钮控件，把它的图片换成虚拟摇杆的图片。在按钮控件中再放一张图片控件，把它的图片换成trackball的图片。

* 2.选中该按钮控件，打开右见菜单“生成组件”，进入高级选项。

* 3.添加事件onInit、onPointerDown、onPointerMove、onPointerUp和onPressed(需要新建该事件)。

* 4.添加一个bool属性eightKeys来表示八向键盘(否则为四向键盘)。

* 5.添加一个Int属性pressRepeat来表示如果按住不放，多长时间重复发送onPressed事件。

* 6.在onInit事件中添加自定义函数(为了防止自定义函数覆盖组件本身的函数，建议给自定义函数的加一个特殊的前缀)。
```
var child = this.getChild(0);
if(child) { 
    child.setAnchor(0.5, 0.5);
}

this.pressedInfo = {};
 
this.computePressedInfo = function(point) {
    var cx = this.w>>1;
    var cy = this.h>>1;
    var cp = {x:cx, y:cy};
    var child = this.getChild(0);
    
    var R = Math.min(cx, cy);
    var r = child ? Math.max(child.w >> 1, child.h >> 1) : 0;   
    var angle = Math.lineAngle(cp, point) * (180/Math.PI);
    var distance = Math.distanceBetween(cp, point);
    
    this.pressedInfo.angle = angle;
    this.pressedInfo.distance = Math.min(distance, R-r);
    
    return this.pressedInfo;
}

this.moveChildToPoint = function(point) {
    var child = this.getChild(0);
    if(!child) { 
        return;
    }
   
   if(!point) {
       child.setPosition(this.w >> 1, this.h>>1);
       return;
   }

    var cx = this.w>>1;
    var cy = this.h>>1;
    var info = this.pressedInfo;
    var r = info.distance;
    var angle = info.angle/(180/Math.PI);
    var x = cx + r * Math.cos(angle);
    var y = cy + r * Math.sin(angle);   
    
    child.setPosition(x, y);
};

this.onTimer = function() {
    if(!this.keyRepeat || !this.pressedPoint) {
        return;
    }
    
    this.dispatchKeyPressed(this.pressedPoint);
    setTimeout(this.onTimer.bind(this), this.keyRepeat);
}

this.dispatchKeyPressed = function(point) {
    var info = this.pressedInfo;
    var angle = info.angle;
    
    if(this.eightKeys) {
        if(angle >= 337.5 || angle < 22.5) {
            info.key = "right";
            info.dx = 1;
            info.dy = 0;
        }
        else if(angle <= 67.5) {
            info.key = "right-down";
            info.dx = 1;
            info.dy = 1;
        }
        else if(angle <= 112.5) {
            info.key = "down";
            info.dx = 0;
            info.dy = 1;
        }  
        else if(angle <= 157.5) {
            info.key = "left-down";
            info.dx = -1;
            info.dy = 1;
        }     
        else if(angle <= 202.5) {
            info.key = "left";
            info.dx = -1;
            info.dy = 0;
        }  
        else if(angle <= 247.5) {
            info.key = "left-up";
            info.dx = -1;
            info.dy = -1;
        }
        else if(angle <= 292.5) {
            info.key = "up";
            info.dx = 0;
            info.dy = -1;
        }        
        else {
            info.key = "right-up";
            info.dx = 1;
            info.dy = -1;            
        }
    }
    else {
        if(angle >= 315 || angle < 45) {
            info.key = "right";
            info.dx = 1;
            info.dy = 0;
        }
        else if(angle <= 135) {
            info.key = "down";
            info.dx = 0;
            info.dy = 1;
        }  
        else if(angle <= 225) {
            info.key = "left";
            info.dx = -1;
            info.dy = 0;
        }  
        else {
            info.key = "up";
            info.dx = 0;
            info.dy = -1;
        }        
    }
    this.dispatchCustomEvent("onKeyPressed", info);
}
```

* 7.处理PointerDown事件。
```
if(beforeChild) {
    return;
}

this.pressedPoint = point;
this.computePressedInfo(point);
this.moveChildToPoint(point);

if(this.keyRepeat) {
    this.onTimer();
}
else {
    this.dispatchKeyPressed(point);
}
```

* 8.处理PointerMove事件。
```
if(beforeChild || !this.pointerDown) {
    return;
}


this.pressedPoint = point;
this.computePressedInfo(point);
this.moveChildToPoint(point);
```
* 9.处理PointerUp事件。
```
if(beforeChild) {
    return;
}

this.moveChildToPoint(null);
this.pressedPoint = null;
```

* 10.使用时只需要处理onKeyPressed事件即可，下面的例子移动场景中的人物，你还可以根据移动的方向切换不同的行走动画。
```
var figure = this.win.find("image");
figure.x += args.dx*2;
figure.y += args.dy*2;
```

事件参数说明：

_args.dx_ 1表示按下位置在中心点的右边。-1表示按下位置在中心点的左边。

_args.dy_ 1表示按下位置在中心点的下边。-1表示按下位置在中心点的上边。

_args.distance_ 表示按下位置与中心点的距离，小于某个值时可以认为点击的中心点。

_args.angle_ 表示按下位置与中心点的角度(度数)。
```
args.dx === 1 && args.dy === 0 表示向右
args.dx === -1 && args.dy === 0 表示向左
args.dx === 0 && args.dy === -1 表示向上
args.dx === 0 && args.dy === 1 表示向下

args.dx === 1 && args.dy === 1 表示向右下
args.dx === 1 && args.dy === -1 表示向左下
args.dx === -1 && args.dy === 1 表示向右上
args.dx === -1 && args.dy === -1 表示向左上
```

[运行效果](http://studio.holaverse.com/apprun.html?appid=previewgithubdrawapp8-cn_release908483a0-c6d7-11e5-b7ca-5b9b8a3da8ed)

[在线编辑](http://studio.holaverse.com/gamebuilder.php?appid=previewgithubdrawapp8-cn_release908483a0-c6d7-11e5-b7ca-5b9b8a3da8ed)
