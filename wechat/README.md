自定义组件实现微信风格的聊天控件
----------------------------------------

* 1.先放一个列表视图控件，勾选列表项高度可以变，把里面的列表项全删除。

* 2.选中该列表视图控件，打开右见菜单“生成组件”，进入高级选项。

* 3.添加事件onInit。

* 4.在onInit事件中添加自定义函数(为了防止自定义函数覆盖组件本身的函数，建议给自定义函数的加一个特殊的前缀)。
```
var leftItem = {
	"type": "ui-list-item",
	"name": "left-item",
	"uid": 19213,
	"z": 0,
	"w": 450,
	"h": 60,
	"pivotX": 0.5,
	"pivotY": 0.5,
	"rotation": 0,
	"opacity": 1,
	"hMargin": 0,
	"vMargin": 0,
	"scaleX": 1,
	"scaleY": 1,
	"roundRadius": 5,
	"runtimeVisible": true,
	"enable": true,
	"visible": true,
	"text": "",
	"x": 0,
	"y": 0,
	"style": {
		"lineWidth": 2,
		"lineColor": "",
		"fillColor": "",
		"textColor": "",
		"fontSize": 16,
		"fontFamily": "serif",
		"focusedFillColor": "",
		"overFillColor": ""
	},
	"xAttr": 0,
	"yAttr": 0,
	"widthAttr": 2,
	"heightAttr": 0,
	"xParam": 1,
	"yParam": 1,
	"widthParam": 1,
	"heightParam": 1,
	"images": {
		"display": 2
	},
	"events": {
		"onClick": null,
		"onLongPress": null,
		"onRemoved": null
	},
	"children": [
		{
			"type": "ui-image",
			"name": "image",
			"uid": 14168,
			"z": 0,
			"w": 40,
			"h": 40,
			"pivotX": 0.5,
			"pivotY": 0.5,
			"rotation": 0,
			"opacity": 1,
			"hMargin": 0,
			"vMargin": 0,
			"scaleX": 1,
			"scaleY": 1,
			"runtimeVisible": true,
			"enable": true,
			"visible": true,
			"text": "",
			"x": 12,
			"y": 7,
			"style": {
				"lineWidth": 2,
				"lineColor": "#7d471b",
				"fillColor": "White",
				"textColor": "Blue",
				"fontSize": 16,
				"fontFamily": "sans"
			},
			"keepSizeWithImage": false,
			"xAttr": 0,
			"yAttr": 0,
			"widthAttr": 0,
			"heightAttr": 0,
			"xParam": 0.02666666666666667,
			"yParam": 1,
			"widthParam": 1,
			"heightParam": 1,
			"imageScaleX": "0.960",
			"imageScaleY": "1.211",
			"images": {
				"display": 4,
				"default_bg": "assets/controls/image.png"
			},
			"events": {
				"onClick": null,
				"onDoubleClick": null,
				"onUpdateTransform": null
			},
			"children": []
		},
		{
			"type": "ui-tips",
			"name": "tips",
			"uid": 11813,
			"z": 2,
			"w": 174,
			"h": 48,
			"pivotX": 0.5,
			"pivotY": 0.5,
			"rotation": 0,
			"opacity": 1,
			"hMargin": 10,
			"vMargin": 10,
			"scaleX": 1,
			"scaleY": 1,
			"roundRadius": 8,
			"runtimeVisible": true,
			"enable": true,
			"visible": true,
			"text": "hello world",
			"x": 88,
			"y": 6,
			"style": {
				"lineWidth": 2,
				"lineColor": "#d0d0d0",
				"fillColor": "#FFFFFF",
				"textColor": "#000000",
				"fontSize": 16,
				"fontFamily": "serif",
				"activeFillColor": "#f5f5f5"
			},
			"clickable": false,
			"triangleSize": 16,
			"hTextAlign": "left",
			"vTextAlign": "middle",
			"xAttr": 0,
			"yAttr": 0,
			"widthAttr": 0,
			"heightAttr": 0,
			"xParam": 0.19555555555555557,
			"yParam": 1,
			"widthParam": 1,
			"heightParam": 1,
			"images": {
				"display": 2
			},
			"events": {
				"onClick": null,
				"onUpdateTransform": null
			},
			"handle": {
				"x": -15,
				"y": 17
			},
			"children": []
		}
	]
};

var rightItem = {
	"type": "ui-list-item",
	"name": "right-item",
	"uid": 19213,
	"z": 1,
	"w": 450,
	"h": 60,
	"pivotX": 0.5,
	"pivotY": 0.5,
	"rotation": 0,
	"opacity": 1,
	"hMargin": 0,
	"vMargin": 0,
	"scaleX": 1,
	"scaleY": 1,
	"roundRadius": 5,
	"runtimeVisible": true,
	"enable": true,
	"visible": true,
	"text": "",
	"locked": false,
	"x": 0,
	"y": 60,
	"style": {
		"lineWidth": 2,
		"lineColor": "",
		"fillColor": "",
		"textColor": "",
		"fontSize": 16,
		"fontFamily": "serif",
		"focusedFillColor": "",
		"overFillColor": ""
	},
	"xAttr": 0,
	"yAttr": 0,
	"widthAttr": 0,
	"heightAttr": 0,
	"xParam": 1,
	"yParam": 1,
	"widthParam": 1,
	"heightParam": 1,
	"images": {
		"display": 2
	},
	"events": {
		"onClick": null,
		"onLongPress": null,
		"onRemoved": null
	},
	"children": [
		{
			"type": "ui-image",
			"name": "image",
			"uid": 14168,
			"z": 0,
			"w": 40,
			"h": 40,
			"pivotX": 0.5,
			"pivotY": 0.5,
			"rotation": 0,
			"opacity": 1,
			"hMargin": 0,
			"vMargin": 0,
			"scaleX": 1,
			"scaleY": 1,
			"runtimeVisible": true,
			"enable": true,
			"visible": true,
			"text": "",
			"x": 393,
			"y": 7,
			"style": {
				"lineWidth": 2,
				"lineColor": "#7d471b",
				"fillColor": "White",
				"textColor": "Blue",
				"fontSize": 16,
				"fontFamily": "sans"
			},
			"keepSizeWithImage": false,
			"xAttr": 0,
			"yAttr": 0,
			"widthAttr": 0,
			"heightAttr": 0,
			"xParam": 0.8733333333333333,
			"yParam": 1,
			"widthParam": 1,
			"heightParam": 1,
			"imageScaleX": "0.960",
			"imageScaleY": "1.211",
			"images": {
				"display": 4,
				"default_bg": "assets/controls/image.png"
			},
			"events": {
				"onClick": null,
				"onDoubleClick": null,
				"onUpdateTransform": null
			},
			"children": []
		},
		{
			"type": "ui-tips",
			"name": "tips",
			"uid": 11813,
			"z": 2,
			"w": 174,
			"h": 48,
			"pivotX": 0.5,
			"pivotY": 0.5,
			"rotation": 0,
			"opacity": 1,
			"hMargin": 10,
			"vMargin": 10,
			"scaleX": 1,
			"scaleY": 1,
			"roundRadius": 8,
			"runtimeVisible": true,
			"enable": true,
			"visible": true,
			"text": "hello world",
			"x": 193,
			"y": 5,
			"style": {
				"lineWidth": 2,
				"lineColor": "#83d45a",
				"fillColor": "#a0e75a",
				"textColor": "#000000",
				"fontSize": 16,
				"fontFamily": "serif",
				"activeFillColor": "#f5f5f5"
			},
			"clickable": false,
			"triangleSize": 16,
			"hTextAlign": "right",
			"vTextAlign": "middle",
			"xAttr": 0,
			"yAttr": 0,
			"widthAttr": 0,
			"heightAttr": 0,
			"xParam": 0.4288888888888889,
			"yParam": 0.08333333333333333,
			"widthParam": 1,
			"heightParam": 1,
			"images": {
				"display": 2
			},
			"events": {
				"onClick": null,
				"onUpdateTransform": null
			},
			"handle": {
				"x": 188,
				"y": 17
			},
			"children": []
		}
	]
};

//=============================================================================
//以上数据通过生成自定义组件获得。
//=============================================================================

this.addItem = function(imgURL, text, atLeft) {
    var json = atLeft ? leftItem : rightItem;
    
    var item = this.addChildWithJson(json);
    var image = item.find("image");
    var tips = item.find("tips");
    
    tips.w = this.w - image.w - 60;
    image.setValue(imgURL);
    tips.setText(text);
    tips.fitToTextContent();
    
    item.w = this.w;
    item.h = Math.max(image.h, tips.h);
    
    tips.y = 0;
    image.y = 0;
    if(atLeft) {
        image.x = 2;
        tips.x = image.w + 20;
        tips.setPointer(-10, 20);
    }
    else {
        var w = item.w;
        var h = item.h;
        
        image.x = w - image.w - 2;
        tips.x = image.x - tips.w - 20;
        tips.setPointer(tips.w+10, 20);
    }
    
    this.relayoutChildren();
    this.scrollToEnd();
}

this.addLeftItem = function(image ,text) {
    this.addItem(image, text, true);
}

this.addRightItem = function(image ,text) {
    this.addItem(image, text, false);
}

this.spacer = 10;

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




