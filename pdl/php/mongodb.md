MongoDB
=======

[Mongo](http://www.php.net/manual/en/class.mongo.php)已停用，可以換使用[MongoClient](http://www.php.net/manual/en/class.mongoclient.php)

階層由大至小為：

    Server -> Database -> Collection -> Data

使用方法：

```php
$m = new MongoClient();
$db = $m->foo;
// $db = $m->selectDB('foo');
```

此時取得的是 [MongoDB](http://www.php.net/manual/en/class.mongodb.php) ，可以對應一般資料庫觀念的 Database

```php
$collection = $db->bar;
// $db = $db-> selectCollection('bar');
```

此時取得的是 [MongoCollection](http://www.php.net/manual/en/class.mongocollection.php) ，可以對應一般資料庫的 Table

如果 collection 做查詢行為的話，會回傳 [MongoCursor](http://www.php.net/manual/en/class.mongocursor.php) 物件

```php
$cursor = $collection->find(array('id' => 1));
```

SQL to MongoDB
--------------

|  SQL  |  MongoDB  |
|  ---  |  -------  |
| CREATE TABLE USERS (a Number, b Number) | Implicit or use MongoDB::createCollection(). |
| INSERT INTO USERS VALUES(1,1) | $db->users->insert(array("a" => 1, "b" => 1)); |
| SELECT a,b FROM users | $db->users->find(array(), array("a" => 1, "b" => 1)); |
| SELECT * FROM users WHERE age=33 | $db->users->find(array("age" => 33)); |
| SELECT a,b FROM users WHERE age=33 | $db->users->find(array("age" => 33), array("a" => 1, "b" => 1)); |
| SELECT a,b FROM users WHERE age=33 | $db->users->find(array("age" => 33), array("a" => 1, "b" => 1)); |
| SELECT a,b FROM users WHERE age=33 ORDER BY name | $db->users->find(array("age" => 33), array("a" => 1, "b" => 1))->sort(array("name" => 1)); |
| SELECT * FROM users WHERE age>33 | $db->users->find(array("age" => array('$gt' => 33))); |
| SELECT * FROM users WHERE age<33 | $db->users->find(array("age" => array('$lt' => 33))); |
| SELECT * FROM users WHERE name LIKE "%Joe%" | $db->users->find(array("name" => new MongoRegex("/Joe/"))); |
| SELECT * FROM users WHERE age>33 AND age<=40 | $db->users->find(array("age" => array('$gt' => 33, '$lte' => 40))); |
| SELECT * FROM users ORDER BY name DESC | $db->users->find()->sort(array("name" => -1)); |
| CREATE INDEX myindexname ON users(name) | $db->users->ensureIndex(array("name" => 1)); |
| CREATE INDEX myindexname ON users(name,ts DESC) | $db->users->ensureIndex(array("name" => 1, "ts" => -1)); |
| SELECT * FROM users WHERE a=1 and b='q' | $db->users->find(array("a" => 1, "b" => "q")); |
| SELECT * FROM users LIMIT 10 SKIP 20 | $db->users->find()->limit(10)->skip(20); |
| SELECT * FROM users WHERE a=1 or b=2 | $db->users->find(array('$or' => array(array("a" => 1), array("b" => 2)))); |
| SELECT * FROM users LIMIT 1 | $db->users->find()->limit(1); |
| EXPLAIN SELECT * FROM users WHERE z=3 | $db->users->find(array("z" => 3))->explain(); |
| SELECT DISTINCT last_name FROM users | $db->command(array("distinct" => "users", "key" => "last_name")); |
| SELECT COUNT(*y) FROM users | $db->users->count(); |
| SELECT COUNT(*y) FROM users where AGE > 30 | $db->users->find(array("age" => array('$gt' => 30)))->count(); |
| SELECT COUNT(AGE) from users | $db->users->find(array("age" => array('$exists' => true)))->count(); |
| UPDATE users SET a=1 WHERE b='q' | $db->users->update(array("b" => "q"), array('$set' => array("a" => 1))); |
| UPDATE users SET a=a+2 WHERE b='q' | $db->users->update(array("b" => "q"), array('$inc => array("a" => 2))); |
| DELETE FROM users WHERE z="abc" | $db->users->remove(array("z" => "abc")); |
