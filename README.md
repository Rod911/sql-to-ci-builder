# Yazan - SQLToCIBuilder
Adavanced SQL to Codeigniter Query Builder Converter written in PHP

### Features
Converts SQL Queries to Codeigniter Query Builder.
Assists on creating optimal query as instructed in Codeigniter Documentation. 
Provides options to interact with, for generating different results.

### Supports 
Codeigniter 3 
Codeigniter 4 

### Demo

##### Online demo
Live demo and free usage will be available soon.

### Get Started
##### Install by manual download: 
Download the repository and install required packages by composer.json :

##### Packagist
You can also install it from packagist by running the following command:
```html
composer install sql-to-ci-builder
```

### Usage
##### Simple example

```php
<?php

use RexShijaku\SQLToCIBuilder;

require_once dirname(__FILE__) . '/../../vendor/autoload.php';

$options = array('civ' => 4);
$converter = new SQLToCIBuilder($options);

$sql = "SELECT COUNT(*) FROM members";
echo $converter->convert($sql);
```
This will produce the following result: 
```php
$this->db->countAll('members');
```
##### A more complex example :

```php
<?php 
$sql = "SELECT * FROM members WHERE age > 30 
                            OR (name LIKE 'J%' OR (surname='P' AND name IS NOT NULL)) AND AGE !=30";
$converter->convert($sql);
```
and this will generate the result below :
```php
$db->table('members')
 ->where('age >',30)
 ->orGroupStart()
     ->like('name','J','after')
     ->orGroupStart()
         ->where('surname','P')
         ->where('name !=',null)
     ->groupEnd()
 ->groupEnd()
 ->where('AGE !=',30)
 ->get();
```
##### Notice 
In both of these examples Codeigniter 4 was used. If you need to change it, or get more comprehensive understanding of provided options then see the following section of Options.
There are dozens of examples for every use case explained in the Query Builder documentation for both version 3 and version 4 located in their respecitve folders inside the <a href="https://github.com/rexshijaku/ChoiceFilter/tree/master/demo">examples</a> folder.

### Options
Some important options are briefly explained below:
| Argument  | DataType    | Default  | Description |
| ----- |:----------:| -----:| -----:|
| civ  | integer | 3 |  Your Codeigniter version. |
| db_instance  |  string | $this->db | Object in which database was loaded and initialized. |
| use_from |   boolean  | false  | In CodeIgniter 3, wether it should use 'from' command instead of 'get' to select data from a table. |
| group |   boolean | true  | Wether it should group key value pairs into a php array, or generate commands for each key value pair. |
| single_line |  boolean  | true |  When this argument is true, then converter tries to generate a single command instead of multiple. |

### How does it works?
Will be explained soon.

### Known issues
Will be explained soon.

### Support
For general questions about Yazan - SQLToCIBuilder, tweet at @rexshijaku or write me an email on rexhepshijaku@gmail.com.
To have a quick tutorial check the examples folder provided in the repository.

### Author
##### Rexhep Shijaku
 - Email : rexhepshijaku@gmail.com
 - Twitter : https://twitter.com/rexshijaku
 
### Thank you
All contributors who created and are continuously improving <a href="hhttps://github.com/greenlion/PHP-SQL-Parser">PHP-SQL-Parser</a>, without it, this project would be much harder to be realized. 

### In memoriam
For the innocent lives lost (including Yazan al-Masri, aged just two) during the 2021 Israel–Palestine crisis.

### License
MIT License

Copyright (c) 2021 | Rexhep Shijaku

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
