自定义组件实现虚拟摇杆(joystick)
----------------------------------------

* 1.在场景中放一个按钮控件，把它的图片换成虚拟摇杆的图片。

* 2.选中该按钮控件，打开右见菜单“生成组件”，进入高级选项。

* 3.添加事件onInit、onPointerDown、onPointerMove、onPointerUp和onPressed(需要新建该事件)。

* 4.添加一个bool属性eightKeys来表示八向键盘(否则为四向键盘)。

* 5.添加一个Int属性pressRepeat来表示，如果按住不放，多长时间重复发送onPressed事件。

* 6.自定义函数。
```
```

