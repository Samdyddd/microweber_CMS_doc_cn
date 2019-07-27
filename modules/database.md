# 保存和获取模块数据


## 定义模式

安装模块时，Microweber检查`config.php`文件中的`$config['tables']`数组。每个键表示一个表名。其值是一个列定义数组。自动创建ID列，默认情况下所有列都为空。

`userfiles/modules/paintings/config.php`

```
$config = array();
$config['name'] = "";
$config['author'] = "";
$config['ui'] = true;
$config['ui_admin'] = true;
$config['position'] = "";
$config['version'] = "";
$config['tables'] = array(
  'paintings' => array(
    'id'=> 'integer',
    'name'=> 'string',
    'price'=> 'float',
    'description'=> 'text',
    'created_by'=> 'integer',
    'created_at'=> 'dateTime',
  )
)

```

## 自定义tables

更多数据存储的选项> http://docs.microweber.com/guides/modules_schema.md

### 获取和保存数据

你可以使用`db_get`,`db_save`,`db_delete`处理表中的数据。

```
$data = db_get("table=paintings")

// save
$save = arry(
  'name'=> 'mono',
  'description'=> 'paiting'
);

$id = db_save('paintings', $save);

// delete
db_delete('paintings', $id);
```

### 创建

`db_save`函数接受表名作为第一个参数，行数据作为第二个参数。为了在表中创建行，不要指定ID。
```
$data = arry(
  'name' => 'three',
  'price'=> 2300,
  'description'=> 'greates'
);
db_save('paintings', $data);
```


### read

调用`db_get`函数并在参数数组中设置表键。

```
$rows = db_get(array('table' => 'paintings'));
```

将参数数组中的单键设置为true，以便函数返回单行。任何保留键名都被视为给定列名的`where`条件。参看`db_get`函数文档。

```
$row = db_get(array(
  'table'=> 'paintings',
  'name' => 'three',
  'single' => true
))

```
可以这样编写以上查询：

```
db_get('table=paintings&name=three&single=true')
```

### update

如果`db_save`函数接收到一个包含id键的数组，将对相应的行执行更新操作。

```
$row = db_get(array(
  'table'=> 'paintings',
  'id' => 3,
  'single'=> true
));

$row['title'] = 'haha';
echo $row['id']
db_save('paintings', $row)

```

### delete

`db_delete`在成功删除具有指定ID的行后返回true.

```
db_delete('paintings', $id = 3);
```










