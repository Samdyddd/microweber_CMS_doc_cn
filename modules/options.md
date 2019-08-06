# module options

函数save_option和get_option用于存储或检索见得的键值数据。每个条目都由其所属的名称和组来标识，这些名称和组作为参数传递。


## gettin options

你可以为每个模块添加自定义选项。例如，现在我们将添加动态文本，它可以从模块设置部分更改。

例子：`userfiles/modules/example_module/index.php`

```
<h1><?php print get_option('mytext', $params['id']); ?></h1>
```

$params['id']值标识当前模块实例id。如果希望从其他组获得选项，可以使用自己的值作为第二个参数。


## 自动保存选项（saving options automatically）

只需将`mw_option_field`类添加到任何输入字段。

例子： `userfiles/modules/example_module/admin.php`

```
<label>
  <input 
    name="text"
    class="mw_option_field"
    type="text"
    value = "<?php print get_option('mytext', $params['id']); ?>"
   />
</label>

```
在admin.php中，你可以使用类`mw_option_field`作为输入字段。当你更改此字段时，它的值将自动保存在数据库中。

输入`name`属性作为`get_option`函数中的键，你可以使用该函数从php检索值。该值保存为当前模块实例。如果希望为另一个实例存储选项，可以在输入字段上设置自定义选项组属性。


## 手动保存选项

通过使用rest api 并调用`save_option`函数，还可以通过ajax保存选项。

例如，现在我们将保存一个名为`text_color`的字段。

`userfiles/modules/example_module/admin.php`


```
<?php $selected_color = get_option('text_color', $params['id']); ?>
<?php $colors = array('red', 'blue', 'green'); ?>

<script>
    $(document).ready(function () {
        $("#my_text_color").change(function () {
            var data = {};
            data.option_group = "<?php print $params['id'] ?>";
            data.option_key = "text_color";
            data.option_value = $(this).val();
            $.post("<?php print api_url('save_option') ?>", data, function (resp) {
                mw.reload_module_parent('#<?php print $params['id'] ?>');
            });
        });
    });
</script>

<select id="my_text_color">
    <option value="" <?php if (!$selected_color): ?> selected="selected" <?php endif; ?>>None</option>
    <?php foreach ($colors as $color): ?>
        <option value="<?php print $color ?>" 
        <?php if ($selected_color == $color): ?> selected="selected" <?php endif; ?>><?php print $color ?></option>
    <?php endforeach; ?>
</select>

```

这些选项是使模块具有动态内容的简单方法。
























