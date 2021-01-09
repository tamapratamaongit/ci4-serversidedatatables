# ci4-serversidedatatables
Server Side Datatables Library for CodeIgniter 4 Framework
**NOTE: This lib is under early development.**

## Description
Library to make server side Datatables on CodeIgniter 4 to be **more easy**

## Disclaimer
This library is based on igniteddatatables and laravel yajra/datatables

## Requirements
* Codeigniter 4.*
* JQuery 3.*
* JQuery Datatables

## Installation
Installation is best done via Composer, you may use the following command:

 Copy file Datatables.php to App/Libraries Folder , if you don't have these folder Just Create one. 


## Disclaimer
This Library based on IgnitedDatatables & laravel yajra/datatables

## Example:
This is an example code for using this library:
* PHP:
```php
<?php namespace App\Controllers;

use App\Libraries\Datatables;

class Home extends BaseController
{
	public function dt()
	{
		 $dt = new Datatables('kategori'); //where kategori is name of table from your database.
     //this library using query builder style. for more information about query builder you can visit https://codeigniter.com/user_guide/database/query_builder.html
     return $dt->where(['deleted_at' => null])
                ->addColumn('action', function ($db) {
                    return "<button title='edit' class='btn btn-sm btn-warning' onclick='edit(\"$id\")'>
                <i class='fa fa-edit'></i></button> 
                <button class='btn btn-sm btn-danger' title='delete' onclick='del(\"$id\")'>
                <i class='fa fa-eraser'></i></button>";
                })->draw();
	}
}
```

* Javascript
```javascript
$('#table').DataTable({
  processing: true,
  serverSide: true,
  ajax:{
    url: 'http://localhost:8080/home/dt'
  },
  columns: [
	  {data: 'username', name: 'username'},
	  {data: 'email', name: 'email'},
	  {data: 'fullname', name: 'fullname'}
	  {data: 'bio', name: 'bio'}
  ]
});
```


## Documentation:

Now you can use this without instantiate class
```php
```

We did not use the POST method due to a problem with the CSRF
```php
$routes->get('datatables/json', 'Controller::method', ['as' => 'dt-json']);
```

* **Select Table**\
	Select the table that you want to use
```php
$dt = new Datatables('kategori');
```
Or
```php
$dt = new Datatables();
$dt->table('kategori')
```


* **Select, where, join etc functionality**\
	for query functionality, this library use query builder style from codeigniter 4 it self. you can visit https://codeigniter.com/user_guide/database/query_builder.html
  for more information

* **Add Column**\
	Select the table that you want to use
 Closure Style
```php
$dt->addColumn('action', function ($db) {
                    $id = $db['kategori_id'];
                    return "<button title='edit' class='btn btn-sm btn-warning' onclick='edit(\"$id\")'>
                <i class='fa fa-edit'></i></button> 
                <button class='btn btn-sm btn-danger' title='delete' onclick='del(\"$id\")'>
                <i class='fa fa-eraser'></i></button>";
                });
```
Or ignited datatables style
```php
$dt = new Datatables();
->addColumn('Actions', "<button title='edit' class='btn btn-sm btn-warning' onclick='edit("$1")'>
                <i class='fa fa-edit'></i></button> 
                <button class='btn btn-sm btn-danger' title='delete' onclick='del("$1")'>
                <i class='fa fa-eraser'></i></button>", 'id');
```

* **Edit Column**\
	Select the table that you want to use
 Closure Style
```php
$dt->editColumn('data_date', function ($db) {
                    return date('d, M Y', strtotime($db['data_date']));
                });
```
Or ignited datatables style
```php
$dt = new Datatables();
->editColumn('data_date', date('d, M Y', strtotime('$1')), 'data_date');
```

### Notes:

* For now, we don't use the POST method due to a problem with the CSRF

<br />

## Author's Profile:

Github: [https://github.com/kusmantopratama]
Facebook: [https://web.facebook.com/k.tamapratama/]
