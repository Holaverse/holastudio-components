自定义组件实现微信风格的聊天控件
----------------------------------------

![chatdemo](https://raw.githubusercontent.com/Holaverse/holastudio-components/master/wechat/chat_demo.png)

* 1.先放一个列表视图控件，勾选列表项高度可变，设置列表项的间距为10。列表项只保留一项，并在里面放一个图片和一个UITips控件，把它们的X/Y/W/H都设置为固定。

* 2.选中该列表视图控件，打开右见菜单“生成组件”，进入高级选项。

* 3.添加事件onInit。

* 4.在onInit事件中添加自定义函数(为了防止自定义函数覆盖组件本身的函数，建议给自定义函数的加一个特殊的前缀)。
```
var templateItem = this.getChild(0);
var json =  templateItem.toJson();
templateItem.remove();

this.addItem = function(imgURL, text, atLeft) {
    var item = this.addChildWithJson(json);
    var image = item.find("image");
    var tips = item.find("tips");
    
    tips.y = 0;
    image.y = 0;
    tips.w = this.w - image.w - 60;
    image.setValue(imgURL);
    tips.setText(text).fitToTextContent();
    item.w = this.w;
    item.h = Math.max(image.h, tips.h);
    
    if(atLeft) {
        image.x = 2;
        tips.x = image.w + 20;
        tips.setPointer(-10, 20).setFillColor("White").setLineColor("#d0d0d0")
    }
    else {
        image.x = item.w - image.w - 2;
        tips.x = image.x - tips.w - 20;
        tips.setPointer(tips.w+10, 20).setLineColor("#83d45a").setFillColor("#a0e75a");
    }
    this.relayoutChildren();
    this.scrollToEnd();
    
    return item;
}

this.addLeftItem = function(image ,text) {
    return this.addItem(image, text, true);
}

this.addRightItem = function(image ,text) {
    return this.addItem(image, text, false);
}

```

使用方法：


显示别人发来的信息调用addLeftItem：
```
var list = this.win.find("list-view");
var str = this.win.find("edit").getText();
list.addLeftItem("images/logos/facebook.png", str);
```

显示自己的信息调用addRightItem:
```
var list = this.win.find("list-view");
var str = this.win.find("edit").getText();
list.addRightItem("images/logos/holaverse-32.jpg", str);
```




