# 多功能按钮的自定义UI

### state-card-button.html
```
什么是Custom_UI? 中文翻译就是 自定义UI
HA的原版UI局限性太大了,一行一个控制.一个空气净化器就要6/7行.太占地方
一个灯光呢?除了开关方便,如果你要调颜色,亮度神马的,都要点开详情页才能实现,太麻烦.
所以就有了Custom_UI=自定义UI.
最早的,也是目前最常用的Custom_UI就是这个了,我们通常叫原版[enter description here](https://github.com/andrey-git/home-assistant-custom-ui)
这个能实现很多功能,也有很多玩法,比如增加圆形徽章组,给灯光增加滑杆直接调亮度,显示更多的信息等...
但是貌似忽略了一些按键功能.
然后我就针对按钮的方便性制作了一个Custom_UI
```

----------

| 作者     | Qinver |
| -------- | ------ |
| E-mail | 770349780@qq.com |
| 版本     | 1.01   |
| 最后更新 |2018年06月02日 19:41:45|

## 目录


		1. [支持的功能](#支持的功能)
			1. [图片展示](#图片展示)
		2. [安装教程](#安装教程)



###  支持的功能
> 一句话慨阔是可以在任意一行ID中增加一些按钮,这些按钮的大小/颜色/图标/状态/功能等都可以自定义,极大的提高了扩展性

 1. 增加按钮时候可以选择本来的控制开关是否隐藏.
 2. 增加的按钮支持方块/文字/图标/自定义图片的显示
 3. 图标和背景方块的颜色支持自定义,且可以根据状态不同改变颜色
 4. 按钮的尺寸、间距、圆角半径均可自定义
 5. 可以在名称下显示附加信息.(这个和原版Custom_UI差不多)
 6. 每一个按钮可以自定义按下的动作,也是就action,和自动化的action功能一样.
>功能简单,但是玩法很多! 
#### 图片展示
 
### 安装教程
1.如果之前没有用过任何的Custom_UI！
那么:下载这个链接里面的两个文件,并放入你的配置文件目录的*==~/custom_components/customizer==*下!

完成第一步就可以使用别人制作的Custom_UI文件了
2.下载我制作的Custom_UI文件(state-card-button.html)放入你的配置目录的 *==~/www/custom_ui==* 下

3.完成以以上两步,那么就安装好了,接下来让它在HA生效
在HA配置文件中对应位置添加以下代码：

``` 
frontend:
  javascript_version: auto
  extra_html_url:
    - /local/custom_ui/state-card-button.html
  extra_html_url_es5:
    - /local/custom_ui/state-card-button.html
```

