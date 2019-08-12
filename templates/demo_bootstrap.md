# template structure

Microweber模板是一组决定网站整体外观的文件。这些文件用于生成站点布局和html代码。

你可以使用php和html使模板尽可能灵活。


## Modules

每个模板由模块组成。你可以将他们视为模板的构建块。

模块的例子有：菜单、帖子列表、联系人表单、购物车、用户登录等。

如果不希望编写自定义功能或重用已编写的代码，可以使用这些模块。

使用模块的标签：`<module type="the_name_of_the_module" template="the_skin_you_want" id="the_id_of_the_module" />`

Post list: 列出博客中所有文章。
Product list: 商店的产品列表
Categories: 所有类别为你的文章或商店
Pictures: 画廊中的照片
Shop: 商店模块
Menu: 菜单模块
Comments: 当前项的注释列表
Social network: 社交网络快捷键

可以在`/userfiles/modules/`查看更多模块信息。


## Layouts

布局是预先定义的简单代码片段，可以添加到页面中。

布局加载了`<module type="some_module_name" />`标记。

### basic files

所有模板都位于`userfiles/templates`目录中。每个模板都包含在自己的文件夹中，在创建新模板时需要创建一个新文件夹。通常，文件夹的名称就是新模板的名称。

模板文件必须是小写的，并且不能包含空格或特殊字符。
最基本模板结构：

```
userfiles
 /templates
    /my_template
     config.php
     editor.php
     header.php
     index.php
     footer.php
     inner.php
     clean.php
```

文件及其用途说明：

config.php: 保存模板的信息，如名称、版本
index.php: 主页默认布局
header.php: site header
footer.php: site footer
clean.php: 页面默认布局
inner.php: post的默认布局
editor.php: 用于在编辑器中可视化页面预览
template_settings.php: 模板的设置


## configuration and tempalte setup

让我们从这里下载模板css文件`https://bootswatch.com/paper/bootstrap.css`，并将其解压到`userfiles/templates/bootswatch_paper`的新文件夹中

解压后，在`userfiles/templates/startbootstrap-agency/config`中创建一个新文件。该文件包含模板名称、作者、版本等信息。

php文件必须包含一个包含以下信息的`$config`数组。

```
<?php
$config = array();
$config['name'] = "Template's name";
$config['author'] = "Your name";
$config['version'] = "0.1";
$config['url'] = "https://github.com/ironsummitmedia/startbootstrap-agency/";
```

## getting to work

现在我们已经有了模板和配置文件，让我们开始工作并将其连接到CMS
当用户进入主页时加载`index.php`文件。您可以在这里看到下载模板的HTML源代码。

我们需要将页眉和页脚分开，这样我们就可以在内部页面布局中重用它们。

### header.php

在`userfiles/templates/startbootstrap-agency/header.php`中创建一个文件，并将模板样式和脚本移动到那里。

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="description" content="">
<meta name="author" content="">
<title>Some Title</title>

<!-- Bootstrap Core CSS -->
<link href="<?php print template_url(); ?>css/bootstrap.min.css" rel="stylesheet">

<!-- Custom CSS -->
<link href="<?php print template_url(); ?>css/agency.css" rel="stylesheet">
<link href="<?php print template_url(); ?>css/custom.css" rel="stylesheet">

<!-- Custom Fonts -->
<link href="<?php print template_url(); ?>font-awesome/css/font-awesome.min.css" rel="stylesheet" type="text/css">
<link href="https://fonts.googleapis.com/css?family=Montserrat:400,700" rel="stylesheet" type="text/css">
<link href='https://fonts.googleapis.com/css?family=Kaushan+Script' rel='stylesheet' type='text/css'>
<link href='https://fonts.googleapis.com/css?family=Droid+Serif:400,700,400italic,700italic' rel='stylesheet' type='text/css'>
<link href='https://fonts.googleapis.com/css?family=Roboto+Slab:400,100,300,700' rel='stylesheet' type='text/css'>

<!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
<!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
<!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
        <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->

</head>

<body id="page-top">

<!-- Navigation -->
<nav class="navbar navbar-default navbar-fixed-top">
  <div class="container">
    <div class="navbar-header page-scroll">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1"> <span class="sr-only">Toggle navigation</span> <span class="icon-bar"></span> <span class="icon-bar"></span> <span class="icon-bar"></span> </button>
      <a class="navbar-brand page-scroll" href="#page-top">Start Bootstrap</a> </div>

    <!-- Include menu module -->
    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <div class=" navbar-right">
        <module type="menu" name="header_menu" id="header_menu" />
      </div>
    </div>

  </div>
</nav>

<!-- Header -->

```

大多数代码应该很简单——我们将html标记放在head部分，并将body的第一部分放在header中。包含`.css`和`.js`文件也非常简单。
对于您使用的`.css`

```
<link href="<?php print template_url(); ?>css/agency.css" rel="stylesheet">
```

```
<?php print template_url(); ?> 
```
是模板的url。别担心，microweber知道该怎么做。.js文件也是如此。使用

```
<script type="text/javascript" src="<?php print template_url('assets/site.js'); ?>"></script>

```

我们正指向文件所在的位置，其余的由Microweber负责。
声明模块也很简单。这里我们说我们想要一个菜单类型的模块，它有一个名字，一个id，我们将在footer。php页面中看到，你也可以分配一个模板。在移动。

### footer.php

和header一样。这将是一个文件，它将是每个页面的一部分，正如它的名字所暗示的，我们将把我们的页脚信息放在里面。

```
<div id="footer">
  <div class="container">
    <div class="edit" rel="global" field="bootstrap3-site-footer">
      <div class="mw-row">
        <div class="mw-col" style="width: 30%">
          <div class="mw-col-container"> <a href="http://facebook.com/Microweber" target="_blank"><img src="<?php print template_url(); ?>img/mw.soc.fb_b.png" /></a> <a href="http://twitter.com/Microweber" target="_blank"><img src="<?php print template_url(); ?>img/mw.soc.tt_b.png" /></a> <a href="http://youtube.com/Microweber" target="_blank"><img src="<?php print template_url(); ?>img/mw.soc.yt_b.png" /></a> </div>
        </div>
        <div class="mw-col" style="width: 70%">
          <div class="mw-col-container">
            <module type="menu" name="footer_menu" id="footer-navigation" template="small" />
          </div>
        </div>
      </div>
    </div>
    <hr>
    <div id="footer-bottom">
      <div class="row">
        <div class="col-md-8">
          <div class="edit" rel="footer" field="footer-copyright">Copyright &copy; <span class="unselectable" contentEditable="false"><?php print date('Y'); ?></span>, All rights reserved </div>
        </div>
        <div class="col-md-4"><span class="muted pull-right"><?php print powered_by_link(); ?></span></div>
      </div>
    </div>
  </div>
</div>
</body></html>
```

代码再次变得尽可能简单。没什么值得注意的!你会看到我们有这个
```
<div class="mw-row">
        <div class="mw-col" style="width: 30%">
          <div class="mw-col-container"> <a href="http://facebook.com/Microweber" target="_blank"><img src="<?php print template_url(); ?>img/mw.soc.fb_b.png" /></a> <a href="http://twitter.com/Microweber" target="_blank"><img src="<?php print template_url(); ?>img/mw.soc.tt_b.png" /></a> <a href="http://youtube.com/Microweber" target="_blank"><img src="<?php print template_url(); ?>img/mw.soc.yt_b.png" /></a> </div>
        </div>
        <div class="mw-col" style="width: 70%">
          <div class="mw-col-container">
            <module type="menu" name="footer_menu" id="footer-navigation" template="small" />
          </div>
        </div>
      </div>
```

注意class="mw-row"和class="mw-col"。这将允许您通过实时编辑器实时调整列的大小。还可以使用style="width:x%"设置初始宽度。
现在你要做的就是使用

```
<?php include template_dir(). "header.php"; ?>
```

```
<?php include template_dir(). "header.php"; ?>
```
将这些文件包含在您希望它们出现的任何地方!

### index.php

```

 <?php

/*

  type: layout
  content_type: static
  name: Home
  position: 11
  description: Home layout

*/

?>
<?php include template_dir(). "header.php"; ?>

<div class="container edit" id="home-layout"  rel="page" field="content">
  <div class="row clearfix">
    <div class="col-md-12 column">
      <div class="jumbotron">
        <h1> Hello, world! </h1>
        <p> This is a template for a simple marketing or informational website. It includes a large callout called the hero unit and three supporting pieces of content. Use it as a starting point to create something more unique. </p>
        <p> <a class="btn btn-primary btn-large" href="#">Learn more</a> </p>
      </div>
    </div>
  </div>
  <div class="mw-row clearfix">
    <div class="mw-col" style="width:33.33%">
      <div class="mw-col-container">
        <div class="element">

          <h2> Heading </h2>
          <p> Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus. Etiam porta sem malesuada magna mollis euismod. Donec sed odio dui. </p>
          <p> <a class="btn" href="#">View details</a> </p>
        </div>
      </div>
    </div>
    <div class="mw-col" style="width:33.33%">
      <div class="mw-col-container">
        <div class="element">
          <h2> Heading </h2>
          <p> Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus. Etiam porta sem malesuada magna mollis euismod. Donec sed odio dui. </p>
          <p> <a class="btn" href="#">View details</a> </p>
        </div>
      </div>
    </div>
    <div class="mw-col" style="width:33.33%">
      <div class="mw-col-container">
        <div class="element">
          <h2> Heading </h2>
          <p> Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus. Etiam porta sem malesuada magna mollis euismod. Donec sed odio dui. </p>
          <p> <a class="btn" href="#">View details</a> </p>
        </div>
      </div>
    </div>
  </div>

  <div class="container">
    <div class="element"> <br>
      <br>
      <h3 align="center" class="symbol">Powerful &nbsp;&amp;&nbsp; User Friendly &nbsp;Content Management System &nbsp;of &nbsp;New Generation</h3>
      <h4 align="center">with rich PHP and JavaScript API</h4>
        <br>
    </div>
  </div>
  <div class="container">
    <div class="mw-row">
      <div class="mw-col" style="width:33.33%">
        <div class="mw-col-container">
          <div class="element">
            <hr class="visible-desktop column-hr">
          </div>
        </div>
      </div>
      <div class="mw-col" style="width:33.33%">
        <div class="mw-col-container">
          <h2 align="center">
            <?php _e("Latest Posts"); ?>
          </h2>
        </div>
      </div>
      <div class="mw-col" style="width:33.33%">
        <div class="mw-col-container">
          <div class="element">
            <hr class="visible-desktop column-hr">
          </div>
        </div>
      </div>
    </div>

    <module
          data-type="posts"
          data-limit="3"
          id="home-posts"
          data-description-length="100"
          data-show="thumbnail,title,created_at,read_more,description"
          data-template="columns" />
  </div>
  <div class="container">
    <div class="mw-row">
      <div class="mw-col" style="width:33.33%">
        <div class="mw-col-container">
          <div class="element">
            <hr class="visible-desktop column-hr">
          </div>
        </div>
      </div>
      <div class="mw-col" style="width:33.33%">
        <div class="mw-col-container">
          <h2 align="center">
            <?php _e("Latest Products"); ?>
          </h2>
        </div>
      </div>
      <div class="mw-col" style="width:33.33%">
        <div class="mw-col-container">
          <div class="element">
            <hr class="visible-desktop column-hr">
          </div>
        </div>
      </div>
    </div>
    <module
          data-type="shop/products"
          data-limit="3"
          id="home-products"

            />
  </div>
</div>
<?php include template_dir().  "footer.php"; ?>
```
这里，我们包括页眉和页脚，在它们之间放一些内容。

```
<?php

/*
type: layout
content_type: static
name: Home
position: 2
is_default: true
description: Clean layout
*/
?>
```
这是给页面一些属性的部分，如名称、描述、类型等。Microweber将仔细分析这一评论，并提取它所需要的一切。在本教程的其余部分中，我们将调用它

```
<?php
/*
file information
*/
```
当使用.edit类时，我们说我们希望包含标记中的元素是可编辑的。有了这些信息，Microweber就会知道，在实时编辑模式下，我们想要对内容有绝对的控制。还应该包括Id、rel和字段，以使字段惟一，并防止不同的编辑字段发生冲突和输出错误。

```
<div class="container edit" id="home-layout"  rel="page" field="content">
.....
</div>
```
更多的功能和解释可以在我们的文档中找到:http://microweber.com/docs/guides/README.md


### clean.php

```
<?php

/*
file information
*/
?>
<?php include template_dir(). "header.php"; ?>
<section id="content">
  <div class="container edit"  field="content" rel="content">
    <p class="element">Type your text here</p>
  </div>
</section>
<?php include template_dir(). "footer.php"; ?>
```
clean页面目的只有一个清除并准备好填充。可以叫他空白页。

### layouts\shop.php

```
<?php

/*
file information
*/

?>
<?php include template_dir(). "header.php"; ?>

<section id="content">
  <div class="container">
    <div class="row" id="shop-products-conteiner">
      <div class="col-sm-12 edit"  field="content" rel="page">
        <p class="p0 element">This text is set by default and is suitable for edit in real time. By default the drag and drop core feature will allow you to position it anywhere on the site. Get creative & Make Web.</p>
      </div>
    </div>
    <div class="row" id="shop-products-conteiner">
      <div class="col-sm-8 edit"  field="content2" rel="page">
        <module type="shop/products"  limit="18" description-length="70"    />
      </div>
      <div class="col-sm-4">
        <?php include template_dir(). 'layouts' . DS."shop_sidebar.php"; ?>
      </div>
    </div>
  </div>
</section>

<?php include template_dir(). "footer.php"; ?>
```

与我们之前看到的所有页面一样，这是Microweber的一个简单而标准的页面。顾名思义，它是为网站的商店部分，其目的是查看主要内容。记住这是主要部分。例如，如果您想为单个产品创建视图，我们可以这样做

```
<?php include template_dir(). "header.php"; ?>

<section id="content">
  <div class="container">
    <div class="row">
      <div class="col-sm-8">
        <h2 class="edit"  field="title" rel="post">Product inner page</h2>
        <hr>
        <div class="edit"  field="content" rel="post">
          <div class="mw-row">
            <div class="mw-col" style="width:50%">
              <div class="mw-col-container">
                <module type="pictures" rel="content" template="product_gallery" />
              </div>
            </div>
            <div class="mw-col" style="width:50%">
              <div class="mw-col-container">
                <div class="product-description">
                  <div class="edit"  field="content_body" rel="post">
                    <p class="element">This text is set by default and is suitable for edit in real time. By default the drag and drop core feature will allow you to position it anywhere on the site. Get creative &amp; <strong style="font-weight: 600">Make Web</strong>.</p>
                  </div>
                  <module type="shop/cart_add" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="edit"  field="related_products" rel="inherit">
          <h4 class="element sidebar-title">Related Products</h4>
          <module type="shop/products"   related="true" />
          <p class="element">&nbsp;</p>
        </div>
      </div>
      <!------------ Sidebar -------------->
      <div class="col-sm-4">
        <?php include_once "shop_sidebar_inner.php"; ?>
      </div>
    </div>
  </div>
</section>
<?php include template_dir(). "footer.php"; ?>
```


注意:为了创建一个连接到主要部分的单视图产品，它必须被称为“theNameOfThePage_inner.php”。“_inner”部分帮助Microweber传输它需要的所有数据，并在指定的字段中显示正确的信息。
如果你想在一个页面中添加一个页面，你可以这样做

```
 <?php include_once "shop_sidebar_inner.php"; ?>
```

### blog.php

为博客创建视图与创建商店布局没什么不同

```
<?php

/*
file information
*/

?>
<?php include template_dir(). "header.php"; ?>

<div id="content">
    <div class="container" id="blog-container">
        <div class="row">
            <div class="col-md-8 " id="blog-main">
                <div class="edit"  field="content" rel="page">
                     <h2>My blog</h2>

                    <p class="p0 element">This text is set by default and is suitable for edit in real time. By default the drag and drop core feature will allow you to position it anywhere on the site. Get creative, Make Web.</p>
                    <module data-type="posts" />
                </div>
            </div>
            <div class="col-md-3 col-md-offset-1" id="blog-sidebar">
                <?php include_once "blog_sidebar.php"; ?>
            </div>
        </div>
    </div>
</div>
<?php include template_dir(). "footer.php"; ?>
```

博客的内页将是:

```
<?php include template_dir(). "header.php"; ?>

<div class="container" id="blog-container">
  <div id="blog-content-<?php print CONTENT_ID; ?>">
    <div class="row">
      <div class="col-sm-9" id="blog-main-inner">
        <h3 class="edit" field="title" rel="content">Page Title</h3>
        <div class="edit post-content" field="content" rel="content">
          <module data-type="pictures" data-template="slider"  rel="content"  />
          <div class="edit"  field="content_body" rel="content">
            <div class="element">
              <p align="justify">This text is set by default and is suitable for edit in real time. By default the drag and drop core feature will allow you to position it anywhere on the site. Get creative, Make Web.</p>
            </div>
          </div>
        </div>
        <div class="edit" rel="content" field="comments">
          <module data-type="comments" data-template="default" data-content-id="<?php print CONTENT_ID; ?>"  />
        </div>
      </div>
      <div class="col-sm-3" id="blog-sidebar">
        <?php  include template_dir(). "layouts/blog_sidebar.php";  ?>
      </div>
    </div>
  </div>
</div>
<?php include   template_dir().  "footer.php"; ?>
```

**Creating other layouts**
有很多方法可以创建布局。您可以将普通HTML代码放在其中，您可以使用模块、预定义的布局或所有提到的内容。这取决于你。请确保检查zip文件中的所有文件以获得更多信息。


## Module skins

你不喜欢现在的皮肤?在微韦伯中，没有什么是永恒的。下面是如何更改模块的外观。
在模板的文件夹中创建一个名为“modules”的文件夹。现在，对于要编辑的每个模块，都要创建一个单独的文件夹。假设我们想为菜单模块创建新的皮肤。我们在“模块”文件夹中创建一个名为“菜单”的文件夹，然后在“菜单”中创建另一个名为“模板”的文件夹。在内部，我们添加了一个新的php文件——让我们将其命名为navbar.php。名字的选择由你决定。在我们把

```
<?php

/*

type: layout

name: Navbar

description: Navigation bar

*/

?>
<script>

$(document).ready(function() {
    $('ul.nav .dropdown').hover(function() {
      $(this).find('.dropdown-menu:first',this).stop(true, true).delay(200).fadeIn();
    }, function() {
      $(this).find('.dropdown-menu:first',this).stop(true, true).delay(200).fadeOut();
    }); 
});

</script>

<div class="navbar-collapse collapse">
  <?php
$menu_filter['ul_class'] = 'nav navbar-nav';
   $menu_filter['ul_class_deep'] = 'dropdown-menu';
 $menu_filter['li_class'] = 'dropdown';

        $mt =  menu_tree($menu_filter);

        if($mt != false){
            print ($mt);
        } else {
            print lnotif("There are no items in the menu <b>".$params['menu-name']. '</b>');
        }
        ?>
</div>
```
如果没有指定皮肤的名称，Microweber将查找一个名为default.php的文件!
就是这样。如果要硬编码模板，必须在模块声明中编写

```
<module type="menu" template="the_name_of_the_file_you_created" id="always_put_unique_id"/>

```
或者，您也可以通过单击您在上面的注释部分中输入的名称，从实时编辑模式中选择它。这是它!

对于引用，您可以进入\userfiles\modules并检查所有您可以访问的模块，其中包含所有这些皮肤。如果您想为它们创建新的皮肤，可以对新模块重复相同的步骤

