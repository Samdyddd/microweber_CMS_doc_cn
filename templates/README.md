# template 指导

microweber模板是一组决定网站整体外观的文件。这些文件用于生成站点布局和html代码。

你可以使用php和html使模板尽可能灵活。


## template 基础

所有模板位于`userfiles/templates`目录中。每个模板都包含在自己的文件夹中，在创建新模板时需要创建一个新文件夹。通常，文件夹的名称被指定为新模板的名称。

模板文件夹必须小写，且补鞥呢包含空格或特殊字符。

最基本模板结构如下：

```
userfiles
  /tempaltes
    /my_tempalte
      config.php
      header.php
      index.php
      footer.php
      clean.php
```

*基本文件和他们的用途*

|文件名| 描述|
|---|---|


config.php: 保存模板的信息（名称、版本）

```
<?php
  $config = array();
  $config['name'] = "my tempalte";
  $config['author'] = "your name";
  $config['version'] = 0.1;
  $config['url'] = "http://xxx.com/";
```

配置文件定义模板的名称，因为它将出现在“tempate selection”菜单和“Settings”区域。

*添加css和javascript*

通常每个模板都有很多文件，css,js,图片文件，你可以将这些文件放在模板文件夹中，并加载到布局文件中。

要添加一些基本样式，请在主题文件夹中创建一个css/文件夹，并在css/theme.css中添加一些css。

```
<!doc html>
<html>
  <head>
    <link rel="stylesheet" href="<?php print tempalte_url();?>"style.css">
    <script type="text/javascript" src="<?php print template_url();?>scripts.js"></script>
  </head>

</html>
```

*添加模块到你的模板中*

如果希望显示动态内容或使用一些自定义功能，可以在模板中添加模块（modules）

模块添加：`<module type="name_of_your_module"/>`

模板函数和常量
Function | Value
|---|---|
template_url() | http://example.com/userfiles/templates/my_template/
template_dir() | /home/user/public_html/userfiles/templates/my_template/

模板变量
varibale | Value
|---| ---|
$content | 当前内容项的数组，可以使page or post
$page    | 当前页面数据的数组
$post    | 当前post数据的数组


## 可编辑区域

可编辑区域是用户可以实时拖放模块和编辑内容的地方。

*如何创建可编辑区域*

你可以在模板中定义可编辑区域，用户可以在其中键入文本和拖放模块，该区域的内容将是动态的，并且可以在包含它的每个布局上进行编辑。

```
<div class="edit" filed="your_region_name" rel="content">
  <p>edit your content</p>
</div>
```








































