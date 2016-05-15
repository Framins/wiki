Hierarchical Structure
======================

多層分類的結構實作方法

The Nested Set Model
--------------------

巢狀分類的實作方法，此模型可以提供的 API 可以參考下面列表：

* insertNode - 新增節點
* updateNode - 更新節點
* deleteNode - 刪除節點
* moveNode - 移動節點
* fullTree - 取得整個樹資料
* getLeafs - 取得末節點
* getPath - 取得根到節點的路徑
* getLevel - 取得節點深度

### Table Structure

必要欄位：

* id - 識別證
* lft - 左子樹
* rgt - 右子樹

可選欄位：

* parent_id - 父節點
* path - 路徑
* level - 深度層級

範例 SQL

```sql
CREATE TABLE IF NOT EXISTS `nestedSet` (
    `id` INT AUTO_INCREMENT PRIMARY KEY,
    `lft` INT NOT NULL,
    `rgt` INT NOT NULL,
    `name` VARCHAR(20) NOT NULL
);
```

Nested set 有個重點是，它需要一個根節點做為開始，而通常這個根節點是不會被使用到的：

```sql
INSERT INTO `nestedSet` (`id`, `lft`, `rgt`, `name`)
VALUES (0, 1, 2, 'root');
```

#### Full Tree

以 rootName 為根，取得整個樹資料

```sql
SELECT node.name
FROM nested_category AS node,
     nested_category AS parent
WHERE node.lft BETWEEN parent.lft AND
      parent.rgt AND 
      parent.name = 'rootName'
ORDER BY node.lft;
```

#### Leaf Nodes

取得末端節點

```sql
SELECT name
FROM nested_category
WHERE rgt = lft + 1;
```

#### Single Path

取得路徑

```sql
SELECT parent.name
FROM nested_category AS node,
     nested_category AS parent
WHERE node.lft BETWEEN parent.lft AND
      parent.rgt AND
      node.name = 'nodeName'
ORDER BY node.lft;
```

Reference
---------

* [MANAGING HIERARCHICAL DATA IN MYSQL](http://mikehillyer.com/articles/managing-hierarchical-data-in-mysql/)
* [用 Nested Set Model 建立巢狀資料表](http://lab.asika.tw/programming/theories-and-concepts/26-nested-set-model.html)
* [nested set model介绍](http://halida.logdown.com/posts/67848-nested-set-model)
