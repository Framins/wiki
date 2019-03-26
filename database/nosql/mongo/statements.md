
SQL to MongoDB Mapping Chart
----------

mongo shell script
--------------
    
```shell
mongo
show dbs
use admin
db  # 列出當前的資料庫名稱
db.auth('root','password')
db.dropDatabase()
show users
 ```

SELECT
-------
MySQL

    SELECT * FROM user

Mongo

    db.user.find()

limit
-----
MySQL

    SELECT * FROM user limit 10,20
     
Mongo

    db.user.find().skip(10).limit(20)


ORDER
-----
MySQL

    SELECT * FROM user ORDER BY age DESC
Mongo
        
    db.user.find().sort({'age': -1})

MySQL

    SELECT COUNT(*) FROM user WHERE `name` = 'starlee'
    
Mongo

    db.user.find({'name' : 'starlee'}).count()

DISTINCT
-----
MySQL

    SELECT DISTINCT(name) FROM user WHERE age > 20
    
Mongo

    db.user.distinct('name', {'age': {$lt : 20}})

WHERE
-----
MySQL

    SELECT * FROM user WHERE name = 'starlee'
    
Mongo
    
    db.user.find({'name' : 'starlee'})
 
AND
----- 
MySQL

    SELECT * FROM people WHERE status = "A" AND age = 50
    
Mongo

    db.people.find({ status: "A", age: 50 })
    
OR    
----- 
MySQL

    SELECT * FROM people WHERE status = "A" OR age = 50
    
Mongo

    db.people.find({ $or: [ { status: "A" } , { age: 50 } ] })
    
IN
-----
MySQL
    
    SELECT * FROM user WHERE `age` IN (25, 35,45)
      
Mongo
    
    db.user.find({'age' : {$in : [25, 35, 45]}})
    
INSERT：
-----
MySQL

    INSERT INOT user (`name`, `age`) values ('starlee',25)
    
Mongo

    db.user.insert({'name' : 'starlee', 'age' : 25})

ALTER
-----
    db.user.insert({'name' : 'starlee', 'age' : 25, 'email' : 'starlee@starlee.com'})

DELETE：
-----
MySQL

    DELETE * FROM user
    
Mongo

    db.user.remove({})

MySQL
    
    DELETE FROM user WHERE age < 30
    
Mongo
    
    db.user.remove({'age' : {$lt : 30}})


UPDATE
-----
MySQL
    
    UPDATE user SET `age` = 36 WHERE `name` = 'starlee'
    
Mongo

    db.user.update({'name' : 'starlee'}, {$set : {'age': 36}})

MySQL

    UPDATE user SET `age` = `age` + 3 WHERE `name` = 'starlee'
     
Mongo

    db.user.update({'name' : 'starlee'}, {$inc : {'age' : 3}})


References
----------

* [SQL 到 MongoDB 對應表](http://calvert.logdown.com/posts/2013/11/14/sql-to-mongodb-mapping-chart)
* [官網 sql-comparison](https://docs.mongodb.com/manual/reference/sql-comparison/)
