---
title: "Join 3 tables"
date: 2018-08-18 20:20:20 -0400
categories: SQL inner join
---

Js:


```sql
CREATE DATABASE sampledb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

use sampledb;

mysql> select * from  store;
+-----+------------+---------+---------+
| sid | store_name | lat     | lng     |
+-----+------------+---------+---------+
|   1 | store1     | 35.1234 | 127.303 |
|   2 | store2     | 35.0928 | 127.113 |
|   3 | store3     | 35.1093 | 127.113 |
|   4 | store4     | 35.2093 | 127.113 |
|   5 | store5     | 35.3093 | 127.113 |
|   6 | store5     | 35.4093 | 127.112 |
|   7 | store6     | 35.5093 | 127.112 |
|   8 | store7     | 35.5093 | 127.112 |
|   9 | store8     | 35.5193 | 127.112 |
+-----+------------+---------+---------+
9 rows in set (0.00 sec)

mysql> select * from complex;
+-----+----------+
| cid | name     |
+-----+----------+
|   1 | complex1 |
|   2 | complex2 |
|   3 | complex3 |
|   4 | complex4 |
+-----+----------+
4 rows in set (0.00 sec)

mysql> select * from layer_map;
+----------+-----+-----+-------+
| layer_id | id1 | id2 | layer |
+----------+-----+-----+-------+
|        1 |   1 |   1 |   102 |
|        2 |   2 |   1 |   102 |
|        3 |   3 |   1 |   102 |
|        4 |   4 |   2 |   102 |
|        5 |   5 |   3 |   102 |
|        6 |   6 |   2 |   102 |
|        7 |   7 |   1 |   102 |
+----------+-----+-----+-------+
7 rows in set (0.00 sec)

mysql> select store.store_name, store.lat, store.lng, complex.name  
        from layer_map 
        inner join store on store.sid = layer_map.id1 
        inner join complex on complex.cid = layer_map.id2 
        where layer = 102 and complex.cid = 1;
+------------+---------+---------+----------+
| store_name | lat     | lng     | name     |
+------------+---------+---------+----------+
| store1     | 35.1234 | 127.303 | complex1 |
| store2     | 35.0928 | 127.113 | complex1 |
| store3     | 35.1093 | 127.113 | complex1 |
| store6     | 35.5093 | 127.112 | complex1 |
+------------+---------+---------+----------+
4 rows in set (0.00 sec)

```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
