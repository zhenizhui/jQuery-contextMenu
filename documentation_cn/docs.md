---
currentMenu: options
---
# Documentation

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [注册一个新的菜单](#register-new-contextmenu)
- [更新菜单的状态](#update-contextmenu-state)
- [选项（在注册新的菜单的时候使用）](#options-at-registration)
  - [selector](#selector)
  - [items](#items)
  - [appendTo](#appendto)
  - [trigger](#trigger)
  - [reposition](#reposition)
  - [delay](#delay)
  - [autoHide](#autohide)
  - [zIndex](#zindex)
  - [className](#classname)
  - [classNames](#classnames)
  - [animation](#animation)
  - [events](#events)
  - [position](#position)
  - [determinePosition](#determineposition)
  - [callback](#callback)
  - [build](#build)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 注册一个新的菜单

使用以下代码来注册一个新的菜单

* 注意：如果想支持SVG的话，使用的jQuery的版本要大于1.12，或者直接使用2.2版本

```javascript
$.contextMenu( options );
```

## 更新菜单的状态

我们可以使用upadate来重新刷新contextMenu的各种状态，包括[禁用](https://swisnl.github.io/jQuery-contextMenu/docs/items.html#disabled)，[隐藏](https://swisnl.github.io/jQuery-contextMenu/docs/items.html#visible)，[图标的设置](https://swisnl.github.io/jQuery-contextMenu/docs/items.html#icon)，[输入的值](https://swisnl.github.io/jQuery-contextMenu/docs/items.html#type)，同时这将调用所有的自定义回调函数

```javascript
$('.context-menu-one').contextMenu('update'); // update single menu
$.contextMenu('update') // update all open menus
```

## 选项（在注册新的菜单的时候使用）

### selector

该字符串用来匹配jQuery选择器。这个选项是必须的。

`selector`: `string` 

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu'
});
```

### items

在菜单里面列出来的[菜单项](docs/item.html)对象。浏览[菜单项](docs/items.html)的详细文档来构建你自己的菜单项

`items`: `object` 一个包含[菜单项](docs/items.html)的对象.

#### 例子
```javascript
$.contextMenu({
    selector: '.context-menu',
    items: {
        copy: {
            name: "Copy",
            callback: function(key, opt){
                alert("Clicked on " + key);
            }
        }
    }
});
```


### appendTo

生成的菜单DOM元素将会插入到指定选择器字符串或者DOM元素的后面（内部的后面）。默认是插入到document.body内部

`appendTo`: `string` or `DOMElement` default: `document.body` 


#### 例子
```javascript
// 用选择器来选择一个容器，这个容器将包含生成的菜单元素
$.contextMenu({
    selector: 'span.context-menu',
    appendTo: 'div#context-menus-container'
});

// 用dom元素来选择一个容器，这个容器将包含生成的菜单元素
var element = document.getElementById('context-menus-container');
$.contextMenu({
    selector: 'span.context-menu',
    appendTo: element
});
```


### trigger

Specifies what event on the element specified in the [selector](#selector) triggers the contextmenu. 

指定[选择器]中指定的元素上的事件（β选择器）触发上下文菜单。

定义如何触发这个菜单

`trigger`: `string` default: `'right'` 


Value | Description
---- | ---- 
`right` | Right mouse button
`left` | Left mouse button
`hover` | Hover the element
`touchstart` | Touchstart only
`none` | No trigger

#### 例子
```javascript

// 通过鼠标左键来触发
$.contextMenu({
    selector: 'span.context-menu',
    trigger: 'left'
});

// 悬浮的时候来触发
$.contextMenu({
    selector: 'span.context-menu',
    trigger: 'hover'
});
```

### hideOnSecondTrigger

Flag denoting if a second trigger should close the menu, as long as the trigger happened on one of the trigger-element's child nodes.  This overrides the reposition option.
            
`hideOnSecondTrigger`: `boolean` default: `false`

### selectableSubMenu

定义菜单项包含的子菜单项能否被点击

`selectableSubMenu`: `boolean` 默认值： `false` 

值 | 描述
---- | ---- 
`true` | All Enabled menu items, even containing others are clickable
`false` | Items containing subitems are not clickable

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    selectableSubMenu: true
});
```

### reposition

Specifies if a menu should be repositioned (`true`) or rebuilt (`false`) if a second [trigger](#trigger) event (like a right click) is performed on the same element (or its children) while the menu is still visible.

`reposition`: `boolean` default: `true` 

值 | 描述
---- | ---- 
`true` | Reposition menu when triggered
`false` | Rebuild menu when triggered

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    reposition: false
});
```


### delay

只对通过“悬浮”[触发](#trigger)菜单这种方式有效。定义菜单出现前的等待时间，单位是毫秒。

`delay`: `int` 默认是：`200`

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    delay: 500
});
```

### autoHide

当鼠标离开触发菜单的元素和菜单项的时候，是否隐藏菜单。

`autoHide`: `boolean` 默认值：`false`

值 | 描述
---- | ---- 
`true` | 鼠标离开的时候隐藏菜单 
`false` | 鼠标离开的时候不要隐藏菜单 

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    autoHide: true
});
```

### zIndex

Specifies the offset to add to the calculated zIndex of the [trigger](#trigger) element. Set to `0` to prevent zIndex manipulation. Can be a function that returns an int to calculate the zIndex on build.

`zIndex`: `int`|`function` default: `1` 

#### Example
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    zIndex: 10
});

$.contextMenu({
    selector: 'span.context-menu',
    zIndex: function($trigger, opt){
        return 120;
});
```

### className

给菜单元素添加额外的CSS类名。如果有多个类名，用空格来分隔

`className`: `string`  

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    className: 'contextmenu-custom contextmenu-custom__highlight'
});
```


### classNames

定义菜单元素的基础样式名。这可以用来更改可能与诸如Bootstrap之类的框架冲突的某些类的类名称。

`classNames`: `object`

```javascript
// 在这里配置一些可能会和别的框架冲突的样式名
var options = {
    classNames : {
    
        hover:            'hover',          // 悬浮菜单项
        disabled:         'disabled',       // 禁用菜单项
        visible:          'visible',        // 隐藏菜单项
        notSelectable:    'not-selectable', // 菜单项不可选中
    
        icon:             'context-menu-icon',           // 基础图标样式
        iconEdit:         'context-menu-icon-edit',
        iconCut:          'context-menu-icon-cut',
        iconCopy:         'context-menu-icon-copy',
        iconPaste:        'context-menu-icon-paste',
        iconDelete:       'context-menu-icon-delete',
        iconAdd:          'context-menu-icon-add',
        iconQuit:         'context-menu-icon-quit',
        iconLoadingClass: 'context-menu-icon-loading'
    
    }
}
```


### animation

动画的属性配置作用在隐藏或者显示菜单的时候。持续时间的单位是毫秒。`show`和`hide`的值特指[jQuery methods](http://api.jquery.com/category/effects/)中一些用来显示和隐藏元素的方法名。

`animation`: `object` default: `{duration: 500, show: 'slideDown', hide: 'slideUp'}` 

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    animation: `{duration: 250, show: 'fadeIn', hide: 'fadeOut'}`
});
```

### events
<!--  @todo runtime options object -->

`show`和`hide`事件在菜单出现前或者隐藏前会被调用。这两个事件发生的上下文都是在触发对象中。This will thus reference the jQuery handle of the [trigger](#trigger) object.

当前菜单的配置选项会传递进来。这个菜单的配置选项是一系列菜单选项的集合并且还包含的菜单的DOM节点。你还可以返回一个`false`来阻断`show`和`hide`函数的调用。

`events`: `object` 

值 | 描述
---- | ---- 
`events.show` | 在菜单出现之前调用
`events.hide` | 在菜单隐藏之前调用
`events.activated` | 在菜单被激活后调用

#### 例子
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    events: {
       show : function(options){
            // 给菜单添加一个类名
            this.addClass('currently-showing-menu');
             
            // 弹出一个提示框
            if( confirm('Open menu with selector ' + options.selector + '?') === true ){
                return true;
            } else {
                // 返回false不让菜单展现出来
                return false;
            }            
       },
       hide : function(options){
           if( confirm('Hide menu with selector ' + options.selector + '?') === true ){
               return true;
           } else {
               // 返回false不让菜单隐藏
               return false;
           }            
       },
       activated : function(options){
               if( confirm('Hide menu with selector ' + options.selector + '?') === true ){
               console.log('Menu Activated');
           }            
       }
});
```

### position
 
通过一个回调函数来改写菜单的位置。该函数的执行环境在触发对象的上下文。
The first argument is the `$menu` jQuery object, which is the menu element. The second and third arguments are `x` and `y` coordinates provided by the `show` event.
第一个参数是`$menu`，它是一个jQuery对象，也就是菜单元素。

The `x` and `y` may either be integers denoting the offset from the top left corner, `undefined`, or the string `"maintain"`. If the string `"maintain"` is provided, the current position of the `$menu` must be used. If the coordinates are `undefined`, appropriate coordinates must be determined. An example of how this can be achieved is provided with [determinePosition](#determinePosition).

`position`: `function(opt.$menu, x, y)`

Value `x` or `y` | Description
---- | ---- 
`int` | Offset in pixels from top-left of trigger element.
`"maintain"` | Maintain current `x` or `y` coordinate
`undefined` | Unknown, [determinePosition](#determinePosition) is called.

#### Example
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    position: function(opt, x, y){
        opt.$menu.css({top: 123, left: 123});
    } 
});
```

### determinePosition

Determine the position of the menu in respect to the given [trigger](#trigger) object, this function is called when there is no `x` and `y` set on the [position](#position) call. 

`determinePosition`: `function(opt.$menu)`  

#### Example
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    determinePosition: function($menu){
        // Position using jQuery.ui.position 
        // http://api.jqueryui.com/position/
        $menu.css('display', 'block')
            .position({ my: "center top", at: "center bottom", of: this, offset: "0 5"})
            .css('display', 'none');
    }
});
```


### callback
<!-- @todo link item.callback -->
Specifies the default callback to be used in case an [item](#items) does not expose its own callback. The default callback behaves just like item.callback.

`callback`: `function(itemKey, opt)` 

#### Example
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    callback: function(itemKey, opt){ 
        // Alert the key of the item and the trigger element's id.
        alert("Clicked on " + itemKey + " on element " + opt.$trigger.attr("id"));
        
        // Do not close the menu after clicking an item
        return false;
    }
});
```

### build

The callback is executed with two arguments given: the jQuery reference to the triggering element and the original contextmenu event. It is executed without context (so this won't refer to anything useful).

If the build callback is found at registration, the menu is not built right away. The menu creation is delayed to the point where the menu is actually called to show. Dynamic menus don't stay in the DOM. After a menu created with build is hidden, its DOM-footprint is destroyed.

With build, only the options [selector](#selector) and [trigger](#trigger) may be specified in the [options](#options-at-registration) object. All other options need to be returned from the build callback.

the build callback may return a boolean false to signal contextMenu to not display a context menu

`build`: `function($triggerElement, event)` 

#### Example
```javascript
$.contextMenu({
    selector: 'span.context-menu',
    build: function($triggerElement, e){
        return {
            callback: function(){},
            items: {
                menuItem: {name: "My on demand menu item"}
            }
        };
    }
});
```

### itemClickEvent

Allows the selection of the `click` event instead of the `mouseup` event to handle the user mouse interaction with the contexMenu. The default event is `mouseup`. Set the option to `"click"` to change to the `click` event.

`itemClickEvent`: `"click"`

This option is global: the first contexMenu registered sets it. To change it afterwards all the contextMenu have to be unregistered  with `$.contextMenu( 'destroy' );` before the change has effect again.  

