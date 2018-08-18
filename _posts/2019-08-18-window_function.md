---
title: "Window function samples"
date: 2018-08-18 20:20:20 -0400
categories: SQL inner join
---

Js:


```sql
mysql> SELECT * FROM goods;
+----+------+----------+-------+
| id | name | category | price |
+----+------+----------+-------+
|  1 | g1   | cat1     |   100 |
|  2 | g2   | cat1     |    50 |
|  3 | g3   | cat2     |   150 |
|  4 | g4   | cat1     |   250 |
|  5 | g5   | cat2     |    62 |
|  6 | g6   | cat1     |   162 |
|  7 | g7   | cat3     |  1962 |
+----+------+----------+-------+
7 rows in set (0.00 sec)


mysql> SELECT *, RANK () OVER (PARTITION BY category ORDER BY price) FROM goods;                                                                           +----+------+----------+-------+-----------------------------------------------------+
| id | name | category | price | RANK () OVER (PARTITION BY category ORDER BY price) |
+----+------+----------+-------+-----------------------------------------------------+
|  2 | g2   | cat1     |    50 |                                                   1 |
|  1 | g1   | cat1     |   100 |                                                   2 |
|  6 | g6   | cat1     |   162 |                                                   3 |
|  4 | g4   | cat1     |   250 |                                                   4 |
|  5 | g5   | cat2     |    62 |                                                   1 |
|  3 | g3   | cat2     |   150 |                                                   2 |
|  7 | g7   | cat3     |  1962 |                                                   1 |
+----+------+----------+-------+-----------------------------------------------------+
7 rows in set (0.00 sec)
```

```sql
mysql> select id, name, category, price, sum(price) over (partition by category order by price desc) as current_sum from goods;
+----+------+----------+-------+-------------+
| id | name | category | price | current_sum |
+----+------+----------+-------+-------------+
|  4 | g4   | cat1     |   250 |         250 |
|  6 | g6   | cat1     |   162 |         412 |
|  1 | g1   | cat1     |   100 |         512 |
|  2 | g2   | cat1     |    50 |         562 |
|  3 | g3   | cat2     |   150 |         150 |
|  5 | g5   | cat2     |    62 |         212 |
|  7 | g7   | cat3     |  1962 |        1962 |
+----+------+----------+-------+-------------+
7 rows in set (0.00 sec)

mysql> select category, sum(price) from goods group by category;
+----------+------------+
| category | sum(price) |
+----------+------------+
| cat1     |        562 |
| cat2     |        212 |
| cat3     |       1962 |
+----------+------------+
3 rows in set (0.00 sec)


```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
