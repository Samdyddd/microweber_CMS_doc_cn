# laravel modules

使用microweber， 你还可以学到laravel框架。你可以按以下操作创建一个具有laravel风格的模块。

创建一个`myposts`的模块，将展示网站内容的列表。


## 1.模块声明

在本地副本中创建这些文件：

`userfiles/modules/myposts/config.php`

```
<?php $config = App\Modules\MyPosts::$config;
```
这个脚本为您的模块设置元数据，如名称、作者、Microweber需要创建的数据库表等。

`userfiles/modules/myposts/index.php`

```
<?php echo (new App\Modules\MyPosts)->render();
```

此脚本呈现模块前端

`userfiles/modules/myposts/admin.php`
```
<?php echo (new App\Modules\MyPosts)->admin();
```

此脚本呈现模块管理页面。
这几乎是您在模块的用户文件中要做的所有工作。我们将使用自动加载来更方便地存储模块代码。注意，我们仍然没有这个App\Modules\MyPosts类。现在我们来创建它。


## 2. 模块类

我们的模块类将包含模块的“入口点”(管理、前端)及其元数据。

`app/Modules/MyPosts.php`

```
<?php namespace App\Modules;
use Content;
class MyPosts {
    static $config = array(
        'name'      => 'My Posts',
        'author'    => 'Ash',
        'ui'        => true,
        'ui_admin'  => true,
        'categories'=> 'general',
        'position'  => 100,
        'version'   => 0.1
        );
    public function render()
    {
        $data = Content::all();
        return view('modules.myposts', compact('data'));
    }
    public function admin() {
        return view('modules.myposts_admin');
    }
}
```

> * `Content`是Microweber雄辩的模型，您可以使用它来处理网站内容存储。
  * 静态数组`$config`是在`config.php`中加载的，而不是硬编码它。
  * 每次在前端显示模块时，都会调用`render`方法。
  * 当模块在管理面板中打开时，将调用`admin`方法。


## module views 

当然，我们的新模块通常必须返回一些响应。您可以使用Laravel的`blade`模板引擎使事情尽可能简单。让我们创建一些示例视图:

`resources/views/modules/myposts.blade.php`

```
<ul>
@foreach($data as $item)
    <li>{{ $item->title }}</li>
@endforeach
</ul>
```
此视图打印内容标题列表。在我们的模块类的`render`方法中，`data`变量作为第二个参数传递给`view()` helper。

当然，如果不需要模板引擎，视图可以是普通的PHP文件。

`resources/views/modules/myposts_admin.php`

```
Welcome to the admin, <b><?php echo Auth::user()->email; ?></b>!
```

4. voila

现在打开您的网站管理面板，并点击扩展->重新(Extensions-> Reload)加载模块(在模块类型下拉框旁边)。一旦模块被重新加载，你会看到我的文章(my posts)在列表中，点击它将带你到它的管理视图。你还可以从实时编辑模式将它拖放到你网站的任何页面上。







