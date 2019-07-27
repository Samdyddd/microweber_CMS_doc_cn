# modules

Micorweber模块时可以防止网站上的php脚本。它们在沙箱环境中执行，但是可以访问Microweber，laravel和任何定制依赖项的功能。模块帮助开发人员进行简单的修改，并向用户页面添加功能。

Microweber附带了一些预装模块，你可以检查和扩展这些模块。我们通过现有代码来学习和创建模块的原则。

大多数情况下，modules是“blocks", 用户可以在网站上需要 的任何地方拖放模块。图库、菜单、显示帖子、列出给定的类别的帖子、联系人表单等。

模块不必依赖于网站内容或设计，可以有自己的表示层。


## 文件结构

每个模块都包含在它自己的`userfiles/modules`文件夹中。为了使新模块可用，你必须打开后端模块管理页面并单击`Reload Modules`。

每个模块需要以下文件才能工作
config.php: 
index.php: 
admin.php:
functions.php:
icon.php:

## 创建一个新模块

执行以下步骤：

1. 创建如`userfiles/modules/example_module/`文件夹
2. 创建`index.php`和`admin.php`文件显示你的模块
3. 创建`config.php`配置你的模块信息

例如`userfiles/modules/example_module/config.php`
```
<?php 
  $config = array();
  $config['name'] = "first my module"
  $config['link'] = "https://git.com"
  $config['description'] = ""
  $config['author'] = "xx"
  $config['ui'] = true; //  可在在线编辑删除该模块
  $config['ui_admin'] = true; // 在管理中可见
  $config['position'] = "98";
  $config['version'] = "0.01";
>

```

## module front-end(模块的前端)

模块文件夹中的`index.php`文件将呈现在用户放置模块的站点上的任何位置。

例子：`userfiles/modules/example_module/index.php`

```
<h1>hello from my module</h1>
```
如果将模块放置在页面上，将看到以上文本。


## module back-end(模块的后端)

用户可以从前端（以模式）或后端访问已安装模块的管理页面。允许用户编辑全局或特定于实例的模块设置。

当用户访问模块管理时，模块根目录中`admin.php`文件将被执行并呈现。

例子：`userfiles/modules/example_module/admin.php`
```
<h2>admin part my module</h2>
```

## using assets

在执行模块时，在它们的作用域中注入一个`$config`数组。它把汗模块路径、名称和其他模块信息。

模块的文件系统位置和url可以在`$config`数组中找到。可以使用它从模块文件夹加载资源或其他脚本。

例子：`userfiles/modules/example_module/index.php`

```
<link rel="stylesheet" href="<?php print $config['url_to_module']; ?>style.css" />

<script src="<?php print $config['url_to_module']; ?>script.js"></script>
```
这个`$config['url_to_module']`包含模块文件夹的完整url(http://<website>.com/userfiles/modules/example_module/)

`$config['path']`包含模块文件夹的完整路径（/var/www/userfiles/modules/example_module

如果在你的模块文件夹中有一个名为`logo.png`的文件，如下代码显示：
```
<img src="<?php echo $config['url_to_module']; ?>logo.png">
```


## 加载模块

在Microweber中，模块时通过模板内的`<module type="your_module_name"/>`标记加载的，其中`type`是模块路径。此外用户还可以在站点的可编辑区域拖放他们。

```
<module type="example_module"/>
```
这段代码将会加载位于`userfiles/modules/example_module/index.php`文件。

若想加载index.php以外文件，如以下：
```
<module type="example_module/something">
```
将会加载`userfiles/modules/example_module/something.php`


## 模块参数

模块可以接受作为html属性传递的参数。

例子：

```
<module type="example_module" my-param="foo" other-parameter="bar" />
```
你可以从`$params`数组访问模块中的参数。在模块文件夹中打开`index.php`并添加此代码。

```
<?php
  $id = $params['id'];
  $foo = $params['my-param'];
  $bar = $params['other-parameter'];

  print("module id:".$id);
  print("parameter is:".$foo);
  print("other is:".$bar);
?>
```
每个模块都有一个'id',$params['id']可以访问它，并且它对于每个模块都是唯一的，除非你将其设置为html属性。如果你不将'id'属性放在模块上，Microweber将生成一个。


## 模块功能

如果在module文件夹中创建一个名为`functions.php`的文件，该文件将在每次请求时自动加载。你可以使用它来创建自定义函数、自动加载类以及做任何喜欢的事情。

检查模块是否处于可编辑模式下：

`userfiles/modules/example_module/index.php`

```
<?php if(in_live_edit()): ?>
<?php  print notif("click here to edit this module"); ?>
<?php endif; ?>
```

以上：
* 在模块中加载其他模块
* 在模块中拥有可编辑区域












































