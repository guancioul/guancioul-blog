---
title: "CodeIgniter 4 資料庫遷移(Migrate)"
categories:
  - Web
tags:
  - Web
  - CodeIgniter 4 
toc: true
published: false
---

網路上有教很多資料庫遷移(Migrate)的方法，但是有很多我看了很久也不是很確定在講什麼，這邊稍微做個筆記整理一下我看到的方法。

## 資料庫遷移是什麼?
在CodeIgniter 4的官方文件上是說，如果今天只有執行SQL，在部屬專案的時候就要記得要先執行這些SQL檔案，要不然資料庫會出問題。

如果用了資料庫遷移，就能夠自動追蹤有哪些資料庫已經被使用過了，避免在部屬的時候發生問題。

## 建立遷移檔案的方法
裝好CodeIgniter 4之後，在cmd的地方打上`php spark`，會出現很多可以用在CodeIgniter 4上面的功能，這邊要講的就是Migration的部分

![image-center]({{site.url}}{{site.baseurl}}/assets/images/CodeIgniter4/w6cZbYX.png){: .align-center}
![image-center]({{site.url}}{{site.baseurl}}/assets/images/CodeIgniter4/rTVIage.png){: .align-center}

先從建立檔案的方式開始，在Generators中會看到make:migration，這個時候如果想要使用但是不會用的話，可以在cmd打上

`php spark help make:migration`

![image-center]({{site.url}}{{site.baseurl}}/assets/images/CodeIgniter4/LnMOAGt.png){: .align-center}

會看到創建Migration的說明，主要是在make:migration後面加上migration的名稱

`php spark make:migration users`

這樣就會建立一個migration的檔案名稱是users

在CodeIgniter 4，Migrations的資料會被放在/app/Database/Migrations的資料夾中

## 使用方法
在[資料庫建構類別](https://monkenwu.github.io/codeIgniter4-taiwan-User-Guide/dbmgmt/forge.html#id7)有詳細的說明，我這邊自己做個筆記

打開文件後，會看到裡面有一個up跟down的function

![image-center]({{site.url}}{{site.baseurl}}/assets/images/CodeIgniter4/pTcHg14.png){: .align-center}

up的部分是在創建table時會做的動作

down則是在刪除table時會做的動作

我這邊要做的是把下面的SQL變成Migration的樣子

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(150),
    email VARCHAR(150),
    password VARCHAR(150),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
) ENGINE=INNODB;
```

### 主鍵(addKey)
一開始要先有一個主鍵
`$this->forge->addKey('id', true)`

下面是addKey的用法
`addKey($key[, $primary = false[, $unique = false]])`

id是主鍵的名稱，後面接上的true就會被設定為是主鍵

### 新增欄位(addField)
```php
$this->forge->addField([
    'name'	=> [
        'type'		=>	'VARCHAR',
        'constraint'	=>	'150',
    ],
]);
```
這邊會有幾個常見的數值要設定
1. type：設定資料型態，常見的有INT、VARCHAR、TEXT等
2. constraint：設定資料的最大長度

剩下的是選用的設定
1. unsigned：定義欄位為unsigned
2. default：定義欄位的預設值
3. null：定義欄位可以是NULL
4. auto_increment：定義欄位的數值會自動增加
5. unique：定義欄位為唯一鍵

以下為參考程式碼
```php
$fields = [
    'id'          => [
        'type'           => 'INT',
        'constraint'     => 5,
        'unsigned'       => true,
        'auto_increment' => true
    ],
    'title'       => [
        'type'           => 'VARCHAR',
        'constraint'     => '100',
        'unique'         => true,
    ],
    'author'      => [
        'type'           =>'VARCHAR',
        'constraint'     => 100,
        'default'        => 'King of Town',
    ],
    'description' => [
        'type'           => 'TEXT',
        'null'           => true,
    ],
    'status'      => [
        'type'           => 'ENUM',
        'constraint'     => ['publish', 'pending', 'draft'],
        'default'        => 'pending',
    ],
];
```

### 完整程式碼
```php
<?php

namespace App\Database\Migrations;

use CodeIgniter\Database\Migration;

class Users extends Migration
{
	public function up()
	{
		$this->forge->addField([
			'name'	=> [
				'type'		=>	'VARCHAR',
				'constraint'	=>	'150',
			],
			'email'	=> [
				'type'		=>	'VARCHAR',
				'constraint'	=>	'150',
			],
			'password'	=> [
				'type'		=>	'VARCHAR',
				'constraint'	=>	'150',
			],
			'created_at datetime default current_timestamp',
		]);
		$this->forge->addKey('id', true);
		$this->forge->createTable('users');
	}

	public function down()
	{
		$this->forge->dropTable('users');
	}
}
```

## 命令列工具(Command)
在[CodeIgniter 4 資料庫遷移](https://monkenwu.github.io/codeIgniter4-taiwan-User-Guide/dbmgmt/migration.html)有詳細的講到作法，這邊我自己做個筆記

### migrate
可以把Migrate的功能應用在資料庫中
```bash
php spark migrate
```

### rollback
取消所有的遷移
```bash
php spark migrate:rollback
```

### refresh
更新資料庫狀態
```bash
php spark migrate:refresh
```

### status
顯示資料庫的詳細資訊
```bash
php spark migrate:status
```

## 參考資料
- [CodeIgniter 4 資料庫遷移](https://monkenwu.github.io/codeIgniter4-taiwan-User-Guide/dbmgmt/migration.html)
- [CodeIgniter 4 資料庫遷移(英文版)](https://codeigniter4.github.io/userguide/dbmgmt/migration.html)
- [資料庫建構類別(forge的用法)](https://monkenwu.github.io/codeIgniter4-taiwan-User-Guide/dbmgmt/forge.html#id7)
- [Database Forge Class](https://codeigniter4.github.io/userguide/dbmgmt/forge.html#adding-keys)
- [How to set Datetime as type for a column on Codeigniter migration](https://stackoverflow.com/questions/42303416/how-to-set-datetime-as-type-for-a-column-on-codeigniter-migration/62369801)
- [Codeigniter 4 Authentication Login and Registration Tutorial](https://www.positronx.io/codeigniter-authentication-login-and-registration-tutorial/) 
