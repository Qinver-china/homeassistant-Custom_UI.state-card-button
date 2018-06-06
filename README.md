# 用于Homeassistant的多功能按钮的自定义UI

### state-card-button.html

什么是Custom_UI? 中文翻译就是 自定义UI  
HA的原版UI局限性太大了,一行一个控制.一个空气净化器就要6/7行.太占地方  
一个灯光呢?除了开关方便,如果你要调颜色,亮度神马的,都要点开详情页才能实现,太麻烦.  
所以就有了Custom_UI=自定义UI.  
最早的,也是目前最常用的Custom_UI就是这个了,我们通常叫原版[Custom_UI](https://github.com/andrey-git/home-assistant-custom-ui "悬停显示")  
这个能实现很多功能,也有很多玩法,比如增加圆形徽章组,给灯光增加滑杆直接调亮度,显示更多的信息等...  
但是貌似忽略了一些按键功能.  
然后我就针对按钮的方便性制作了一个`Custom_UI.state-card-button`

----------

| 作者     | Qinver |
| -------- | ------ |
| E-mail | 770349780@qq.com |
| 版本     | 1.01   |
| 最后更新 |2018年06月03日 10:50|

## 目录

* [支持的功能](#支持的功能)
	* [图片展示](#图片展示)
* [安装教程](#安装教程)
  * [准备](#准备-如果之前没有用过任何的custom_ui)
  * [安装](#安装state-card-buttonhtml)
  * [激活](#激活完成以以上两步那么就安装好了接下来让它在ha生效)
* [配置文件格式](#配置文件格式)
 	* [完整的配置格式](#完整的配置格式)
 	* [按钮样式](#按钮样式)
 	 * [原按钮是否显示](#原按钮是否显示)
 	 * [附加信息显示](#附加信息显示)
 	* [自定义按钮功能](#自定义按钮功能)
* [注意事项](#注意事项)
* [帮助与支持](#帮助与支持)

----------

###  支持的功能
 一句话慨阔是可以在任意一行ID中增加一些按钮,这些按钮的大小/颜色/图标/状态/功能等都可以自定义,极大的提高了扩展性
```
 1. 增加按钮时候可以选择本来的控制开关是否隐藏.
 2. 增加的按钮支持方块/文字/图标/自定义图片的显示
 3. 图标和背景方块的颜色支持自定义,且可以根据状态不同改变颜色
 4. 按钮的尺寸、间距、圆角半径均可自定义
 5. 可以在名称下显示附加信息.(这个和原版Custom_UI差不多)
 6. 每一个按钮可以自定义按下的动作,也是就action,和自动化的action功能一样.
 ```
**功能简单,但是玩法很多!** 
#### 图片展示  
![!](/screenshot/效果图.jpg "效果图")
### 安装教程
#### 准备: 如果之前没有用过任何的Custom_UI！  
那么:下载[**这个链接**](https://github.com/andrey-git/home-assistant-customizer/tree/master/customizer)里面的两个文件,并放入你的配置文件目录的`~/custom_components/customizer`下!  
![!](/screenshot/安装1.jpg "")  
完成第一步就可以使用别人制作的Custom_UI文件了

#### 安装state-card-button.html
下载我制作的Custom_UI文件[**(state-card-button.html)**](https://github.com/Qinver-china/homeassistant-Custom_UI.state-card-button/blob/master/www/custom_ui/state-card-button.html)放入你的配置目录的`~/www/custom_ui`下.  
![!](/screenshot/安装2.jpg "")

#### 激活:完成以以上两步,那么就安装好了,接下来让它在HA生效
在HA`configuration.yaml`配置文件中对应位置添加以下代码：

```yaml 
frontend:
  javascript_version: auto
  extra_html_url:
    - /local/custom_ui/state-card-button.html
  extra_html_url_es5:
    - /local/custom_ui/state-card-button.html
```

----------


### 配置文件格式
#### 完整的配置格式
以下是一个完整的配置格式,当然一般情况不需要这么齐全,请阅读注释内容以做编辑

```yaml
#下面是一个完整的配置写法,可能大多数都不会完全用的上,可以直接注释掉或者删除!
#下面注释中凡是写了默认值的,都是可以删除的!删除不写就是默认值!
homeassistant:
  customize:
    input_boolean.boolean_ceshi2:            ###主ID
      friendly_name: 这是我的名字
      icon: mdi:fan    ###主图标
      custom_ui_state_card: state-card-button    ##要用这个custom_ui,就必须写这个!
      config:
        width: 70px                 # 宽度，低于35px无效，默认为35px
        height: 35px                # 高度，低于35px无效，默认为35px
        border_radius: 10px        # 圆角半径（默认为5px）
        gap: 10px                   # 间距（默认为8px）
#以上几个都建议可以不写,保持默认值就行!
        ha_entity_toggle_display: none       # 不显示右边本来的按钮（默认为显示）
        extra_badge:                         #在设备名称下方显示其他附加信息(默认不显示)
          - entity_id: light.led_tasmota     #在设备名称后显示其他设备信息的ID
            title: 亮度                       #显示的前文本(默认不显示))
            attribute: brightness            #若加此项则显示该设备的附加属性(默认显示state值)
            unit: '%'                        #单位(也就是后文本,默认不显示)
          - entity_id: input_boolean.boolean_ceshi2   #可以写多个id的信息,默认就是这个ID的state值
##下面开始写按钮了!
        entities:
          - entity: input_boolean.boolean_ceshi3       #增加的按钮的entity_id
            label: 风类                   #这个按钮显示的文字内容!(默认不显示文字)
            icon: mdi:home-outline        #这个按钮显示的图标(默认不显示)
            image: 'https://www.easyicon.net/api/resizeApi.php?id=1210167&size=48'         #这个按钮的背景图片,地址格式可以为全连接.或者将图片放在www文件下,就像模板这样写!支持多中图片格式,甚至是GIF! 但注意尺寸!并且写了这个那么下面的背景颜色将失效!
            image_height: 35px            #背景图片高度,默认为24px,和icon同尺寸.写 auto ,为图像本身大小.(写了image才需要写这个,或者不写就为默认)
##以上三个显示为文字/图标/图片,可选择,建议三选一.当然也可以全部选!
            background_color_off: 'var(--paper-toggle-button-checked-button-color)'    # 按钮方块背景颜色-关闭的时候(默认为透明)
            background_color_on: 'var(--paper-toggle-button-checked-button-color)'     # 按钮方块背景颜色-打开的时候(默认为透明)
            color_on: 'var(--primary-text-color)'               # 图标和文字的颜色-打开的时候(默认为主题按钮颜色)
            color_off: 'var(--primary-text-color)'              # 图标和文字的颜色-关闭的时候(默认为主题按钮颜色)
##上面的颜色,以及颜色随状态改变. 颜色的写法为CSS颜色格式.比如 '#FFFFFF' / 'rgba(129, 176, 128,0.6)' .也可以为css变量.我上面的模板就是用的变量,直接引用的主题颜色,这样就可以随主题切换!
            service: light.turn_on         #当这个按钮点击时候的动作,也就是action.(默认为toggle)
            data:                          #如果需要发送data就写,写法和自动化的action差不多!(默认没有)
              entity_id: light.led_tasmota  #如果有写data就必须写entity_id,不写就是控制全部 light
              rgb_color: [255,0,0]
              brightness: 200
#按钮点击时候的动作,也就是action.写法和自动化的action差不多! 不会的搜索自动化教程!  当然也可以不写,不写就是单纯的按钮动作!
          - entity: input_boolean.boolean_ceshi4   #可以加多个按钮,就像上面格式这样写!
            image: 'https://www.easyicon.net/api/resizeApi.php?id=1210201&size=48'         #这个按钮的背景图片,地址格式可以为全连接.或者将图片放在www文件下,就像模板这样写!支持多中图片格式,甚至是GIF! 但注意尺寸!并且写了这个那么下面的背景颜色将失效!
            image_height: 30px            #背景图片高度,默认为24px,和icon同尺寸.写 auto ,为图像本身大小.(写了image才需要写这个,或者不写就为默认)

######最后注意!由于我上面写的是完整的配置,所以直接用效果肯定不好,很多其实没必要都写,自己多试试,多一些组合就有更多的玩法! 
###另外由于上面注释很多! 一定要看准对齐喔!
```
#### 按钮样式
按钮可以显示为背景/图标/文字/图片的各种组合.  
背景和图标文字的颜色可以分别设置开和关的颜色,以达到状态反馈  
按钮可以自定义尺寸和圆角半径,可以实现显示为圆形  
```yaml
~~~
      config:
        width: 70px                 # 宽度，低于35px无效，默认为35px
        height: 35px                # 高度，低于35px无效，默认为35px
        border_radius: 10px        # 圆角半径（默认为5px）
        gap: 10px                   # 间距（默认为8px）
        entities:
          - entity: input_boolean.boolean_ceshi3       #增加的按钮的entity_id
            label: 风类                   #这个按钮显示的文字内容!(默认不显示文字)
            icon: mdi:home-outline        #这个按钮显示的图标(默认不显示)
            image: 'https://www.easyicon.net/api/resizeApi.php?id=1210167&size=48'         #这个按钮的背景图片,地址格式可以为全连接.或者将图片放在www文件下,就像模板这样写!支持多中图片格式,甚至是GIF! 但注意尺寸!
            image_height: 35px            #背景图片高度,默认为24px,和icon同尺寸.写 auto ,为图像本身大小.(写了image才需要写这个,或者不写就为默认)
##以上三个显示为文字/图标/图片,可选择,建议三选一.当然也可以全部选!
            background_color_off: 'var(--paper-toggle-button-checked-button-color)'    # 按钮方块背景颜色-关闭的时候(默认为透明)
            background_color_on: 'var(--paper-toggle-button-checked-button-color)'     # 按钮方块背景颜色-打开的时候(默认为透明)
            color_on: 'var(--primary-text-color)'               # 图标和文字的颜色-打开的时候(默认为主题按钮颜色)
            color_off: 'var(--primary-text-color)'              # 图标和文字的颜色-关闭的时候(默认为主题按钮颜色)
```
#### 原按钮是否显示
是否显示这个ID右边原有的开关按钮,默认为显示,如果需要不显示,则添加以下配置
```yaml
~~~
      config:
        ha_entity_toggle_display: none       # 不显示右边本来的按钮（默认为显示）
```

#### 附加信息显示
可以在名称下方显示一些附加的信息
```yaml
~~~
      config:
        ha_entity_toggle_display: none       # 不显示右边本来的按钮（默认为显示）
        extra_badge:                         #在设备名称下方显示其他附加信息(默认不显示)
          - entity_id: light.led_tasmota     #在设备名称后显示其他设备信息的ID
            title: 亮度                       #显示的前文本(默认不显示))
            attribute: brightness            #若加此项则显示该设备的附加属性(默认显示state值)
            unit: '%'                        #单位(也就是后文本,默认不显示)
          - entity_id: input_boolean.boolean_ceshi2   #可以写多个id的信息,默认就是这个ID的state值
```
#### 自定义按钮功能
按钮点击时候的动作,也就是`action`.写法和自动化的action差不多! 不会的搜索自动化教程!  当然也可以不写,不写就是单纯的按钮toggle动作!
```yaml
~~~
      config:
        entities:
          - entity: input_boolean.boolean_ceshi3       #增加的按钮的entity_id
            icon: mdi:home-outline
            service: light.turn_on                #当这个按钮点击时候的动作,也就是action.(默认为toggle)
            data:                           #如果需要发送data就写,写法和自动化的action差不多!(默认没有)
              entity_id: light.led_tasmota           #如果有写data就必须写entity_id,不写就是控制全部 light
              rgb_color: [255,0,0]
              brightness: 200
          - entity: climate.midea
            image: 'https://www.easyicon.net/api/resizeApi.php?id=1181722&size=48'
            image_height: 26px 
            service: climate.set_operation_mode
            data:
              entity_id: climate.midea  #如果有写data就必须写entity_id,不写就是控制全部climate
              operation_mode: auto 
```


----------


### 注意事项

 - 注意添加的按钮数量以及宽度,如果太长可能会造成显示不佳


----------


### 帮助与支持
欢迎加入[『瀚思彼岸』](https://bbs.hassbian.com)论坛  
我在论坛中的[其它主题](https://bbs.hassbian.com/home.php?mod=space&uid=645&do=thread&view=me&from=space) ,以及联系方式  
如果遇到问题请在[这个帖子](https://bbs.hassbian.com/thread-3921-1-1.html)中提交回复

