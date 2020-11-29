---
title: 转载：被leader喷对MySQL索引一无所知的我是如何一小时掌握MySQL索引
date: 2020-11-29 13:15:08
categories: 转载分享
tags:
	- 转载
description: 转载自掘金：https://juejin.cn/post/6900129302285647879
cover: https://upyun-cdn.mistill.com/img/post_cover/post_cover_029.webp
abbrlink: reprint-201129

---

{% note info flat %}
转载自思否：https://juejin.cn/post/6900129302285647879
{% endnote %}



今天被leader喷我对索引一无所知，气的我直接花了一个小时时间把MySQL的索引从头到尾看了一遍，准备去吊打leader去

我：领导啊，我中午没午休，看了一个小时的索引，现在终于把MySQL的索引给精通了。

leader：诶呦，小伙子口气不小啊。来，那我来考考你

leader：那你就先来说说，索引到底是个什么东西吧？

我：网上和书上都说索引是快速查询的数据结构。但是我觉得，这么回答其实并不是完全正确的。

# 什么是索引？

首先来给大家看三个图 ![img](https://upyun-cdn.mistill.com/img/post_img/168cbb9fb64d43f89d1f76e8fff8a660~tplv-k3u1fbpfcp-watermark.image)

![img](https://upyun-cdn.mistill.com/img/post_img/43a02c1a9f4346b1bedfc9f10a16cb2b~tplv-k3u1fbpfcp-watermark.image) 

![img](https://upyun-cdn.mistill.com/img/post_img/821c177f2e3c4644b76393c0e4e05e8c~tplv-k3u1fbpfcp-watermark.image) 对磁盘读取了解的小伙伴一定知道，他读数据是怎么一个原理，如果不了解的，建议去百度一下，大概了解一下再来看接下来的，虽然看上图，是顺序的，但是在磁盘中，他却不是顺序存储的 在磁盘中，如果想要找到数据的话，需要两个步骤：

1. 第一个是比如找到柱面，即刺头需要移动到对准相应的磁道，这个过程叫做寻道，这个过程需要耗费的时间叫做寻道时间。
2. 第二个就是目标扇区旋转到磁头下，即磁盘旋转将目标扇区旋转到磁头下。这个过程耗费的时间叫做旋转时间。

寻道这个过程是很浪费时间的，所以，有没有什么办法，能快速的读取磁盘中的数据呢？

那么，我们可以想到的是二叉树。 ![img](https://upyun-cdn.mistill.com/img/post_img/bba6da05abfb43aeb70cb38e2747c2c2~tplv-k3u1fbpfcp-watermark.image) 二叉树的特性大家应该都清楚，这里就不多说了，这里如果想找23的话，首先从34这个节点开始找，走到22，之后再走到23，那么这里就是进行了三次的磁盘IO就找到了，如果不用索引的话，从34找到23，就需要7次的磁盘IO，直接减少了四次，这里还只是7条数据，如果是7百万的数据呢？效果会更好，更快

那么想一下，二叉树有什么缺点呢？ 再给大家看一个图 ![img](https://upyun-cdn.mistill.com/img/post_img/1dcc84a946644418bd74dcae9596a4cc~tplv-k3u1fbpfcp-watermark.image)

如果是用Col1做二叉树的节点，那么就会变成这样，这就变成了一个链表了，那么这样查询的效率还是很低，如果想要找23的话，还是需要7次磁盘IO

第二个缺点就是，二叉树的节点还是太多了，如果数据量比较大的情况下，虽然会比正常情况下大大减少了IO的读取次数，但是还是要进行非常多次的IO操作

那么想一下，为了解决第一个问题，我们可以想到红黑树 ![img](https://upyun-cdn.mistill.com/img/post_img/5c594f9fd4e54db487d8ddf4986342be~tplv-k3u1fbpfcp-watermark.image) 红黑树是一个平衡二叉树，通过设置红黑节点，节点的旋转来让树平衡，而不会变成链表。但是红黑树还是会存在上面说的第二个缺点。

这个时候肯定会有人想到了，Hash啊，Hash想要搜索一个数据的话，就需要进行一次Hash运算，非常的快，之后进行一次磁盘IO就ok了

那么Hash也是有缺点的，就是Hash只支持单值查询，并不支持范围查询，那么如果想要进行范围查询Hash就用不了了。

上面这些缺点的话，有一个数据结构可以把这些缺点都解决，那么这个数据机构就是B树 ![img](https://upyun-cdn.mistill.com/img/post_img/62a7a0065aa7499792af0c99efa0c976~tplv-k3u1fbpfcp-watermark.image) B树都有哪些特征呢？ 可以看到上图中，B树实际上就是二叉树做了一个横向扩展，而且是kv的形式，每个节点都对应着一个data，这样的话，假如想要查询49的data其实只需要一次磁盘IO就可以了，非常的快非常的高效，在这个讲究的快（除了男生某方面讲究越慢越好）的时代，我觉得B树非常不错了。

那么还有什么数据结构比B树还要好呢？B树就没有缺陷么？

B树的不管是叶子节点还是非叶子节点上的节点都带有data，如果没记错的话，MySQL的一个节点设置的大小是16k，那么就是说明，这个非叶子节点上带着data比较大的话，节点上节点就会比较少了，如果data中存在文本数据的话，大家想想，这又一个节点没几个数据了

所以，这个时候B+树就出现了，B+树解决了B树的这些缺点 ![img](https://upyun-cdn.mistill.com/img/post_img/8bd3c02a3bc744838fc6d022cc988601~tplv-k3u1fbpfcp-watermark.image) B+树相对于B树来说：

1. 非叶子节点是不存储数据的，仅存储键值，这样，就可以存储更多的键值，树就会"更矮更胖",IO的次数就会更少，效率就会更高
2. 这里的页是双向链表链接，这个图有点不太对，data是通过单向链表链接
3. 这里还会做键冗余，冗余到叶子节点上，是为了赋值。

如果想要查询49元素，那么我只需要做三次IO，第一次IO，然后查询到这一段数据，可以通过二分查找，可以从头循环遍历，然后找到这个范围值往下找，再进行一次IO，之后重复上述的操作，再进行一次IO找到49的data

PS：上面说到的数据结构，之后的文章都会讲，后面会单独出一个数据结构和算法的章节，并且会讲一些Leetcode上的题

所以总结一下：什么是索引？

索引就是依靠某些数据结构和算法来组织数据，最终引导用户快速检索出需要的数据，索引的本质就是通过不断的缩小想要获取数据的范围来筛选出最终想要的结果，同时吧随机的事件变成顺序的事件，也就是说，有了这种索引机制，我们可以总是用同一种查找方式来锁定数据。

leader：可以，小伙子，学习的不错，上面的还是偏简单呢，下面再问你一个难的？

我：来吧，无所畏惧！

leader：那你说一下，索引的种类吧？

我：这也难不倒我嘛。

# 索引的种类

这里可以从4个方向来划分索引：

1. 从索引存储结构划分：B+Tree索引，Hash索引，FULLTEXT索引，R Tree索引
2. 从应用层次划分：普通索引，唯一索引，主键索引，复合索引
3. 从索引键值类型划分：主键索引，辅助索引（二级索引）
4. 从数据存储和索引键值逻辑关系划分：聚集索引，非聚集索引

## 普通索引

这是最基本的索引，基于普通字段建立索引，没有任何限制

创建方式：

- CREATE INDEX <索引的名字> ON tablename (字段名);
- ALTER TABLE tablename ADD INDEX [索引的名字] (字段名);
- CREATE TABLE tablename ( [...], INDEX [索引的名字] (字段名) );

## 唯一索引

与普通索引类似，不同的就是：索引字段的值必须是唯一，但是允许有空值。在创建或修改表时追加唯一约束，就会自动创建对应的唯一索引。

创建方式：

- CREATE UNIQUE INDEX <索引的名字> ON tablename (字段名);
- ALTER TABLE tablename ADD UNIQUE INDEX [索引的名字] (字段名);
- CREATE TABLE tablename ( [...], UNIQUE [索引的名字] (字段名) ;

## 主键索引

它是唯一特殊的唯一索引，不允许有空值。在创建或修改表时追加主键约束即可，每个表只能有一个主键

创建方式：

- CREATE TABLE tablename ( [...], PRIMARY KEY (字段名) );
- ALTER TABLE tablename ADD PRIMARY KEY (字段名);

## 复合索引

单一索引是指索引列为一列的情况，也就是说新建索引的语句只能实施在一列上，用户可以在多个列上建立索引，这种索引叫做复合索引。复合索引可以代替多个单一索引，相比多个单一索引复合索引所需的开销更小。

创建方式：

- CREATE INDEX <索引的名字> ON tablename (字段名1，字段名2...);
- ALTER TABLE tablename ADD INDEX [索引的名字] (字段名1，字段名2...);
- CREATE TABLE tablename ( [...], INDEX [索引的名字] (字段名1，字段名2...) );

复合索引使用注意事项：

- 何时使用复合索引，要根据where条件建索引，注意不要过多使用索引，过多使用会对更新操作效率有很大的影响。
- 如果表已经建立了（col1，col2），就没有必要再单独建立（col1）；如果现在有（col1）索引，如果查询需要col1和col2条件，可以直接建立（col1，col2）复合索引，对于查询有一定的提高。

## 全文索引

查询操作在数据量比较少时，可以使用like模糊查询，但是对于大量的文本数据检索，效率很低。如果使用全文索引，查询速度会like快很多倍。在MySQL5.6以前的版本，只有MyISAM存储引擎支持全文索引，从MySQL5.6以前的版本，只有MyISAM存储索引支持全文检索，从MySQL5.6开始MyISAM和InnoDB存储引擎支持。

创建方式：

- CREATE FULLTEXT INDEX <索引的名字> ON tablename (字段名);
- ALTER TABLE tablename ADD FULLTEXT [索引的名字] (字段名);
- CREATE TABLE tablename ( [...], FULLTEXT KEY [索引的名字] (字段名) ;

和常用的like模糊查询不同，全文索引有自己的语法格式，使用match和against关键字，比如

```sql
select * from user
 where match(name) against('aaa');
复制代码
```

全文索引使用注意事项：

- 全文索引必须在字符串，文本字段上建立
- 全文索引字段值必须在最小字符和最大字符之间的才会有效（innodb：3-84；myisam：4-84）
- 全文索引字段值要进行切词处理，按syntax字符进行切割，例如b+aaa，切分成b和aaa
- 全文索引匹配查询，默认使用的是的等值匹配，例如a匹配a，不会匹配ab，ac。如果想匹配可以在布尔模式下搜索a*

leader：回答的不错嘛，那么接下来你再跟我说一下，什么是聚集索引，什么是非聚集索引？

我：这。。。。我得想一想。。。。，啊，想起来了，听我一一道来

# 聚集索引和非聚集索引

B+Tree的叶子节点存放主键索引值和行记录就属于聚集索引；如果索引值和行记录分开存放就数据非聚集索引

## 聚集索引

聚集索引是一种数据存储方式，InnoDB的聚集索引就是按照主键顺序构建B+Tree结构。B+Tree的叶子节点就是行记录，行记录和主键值紧凑地存储在一起。这也意味着InnoDB的主键索引就是数据表本身，它按主键顺序存放整张表的数据，占用的空间就是整个表数据量的大小。通常说的主键索引就是聚集索引。

InnoDB的表要求必须要有聚集索引：

- 如果表定义了主键，则主键索引就是聚集索引
- 如果表没有定义主键，则第一个非空unique列作为聚集索引
- 否则InnoDB会从建一个隐藏row-id作为聚集索引

## 辅助索引

InnoDB辅助索引也叫二级索引，是根据索引构建B+Tree结构。但在B+Tree的叶子节点中只存了索引列和主键信息。二级索引占用的空间会比聚集索引小很多，通常创建辅助索引就是为了提升查询效率。一个表InnoDB只能创建一个聚集索引，但可以创建多个辅助索引。 ![img](https://upyun-cdn.mistill.com/img/post_img/3aed591cecd34150acb2e85d4d5cafe1_tplv-k3u1fbpfcp-watermark.png) 看上图，简单分析一下流程，就是比如一个where条件时name=Elison，这个name有辅助索引，那么他就会先去这个记录name的索引树中找到Elison这个节点，这个时候就会得到Id，再根据这个Id，查询主键索引，找到Id为7的节点，从而找到所有参数。

## 非聚集索引

非聚集索引只适用于MyISAM，因为MyISAM的数据表的索引文件和数据文件是分开的 ![img](https://upyun-cdn.mistill.com/img/post_img/966b9bb41f944cc5ab1333cba9d34d99_tplv-k3u1fbpfcp-watermark.png) PS：关于InnoDB和MyISAM之后的章节会讲 聚集索引和非聚集索引的区别主要是在InnoDB和MyISAM的区别，因为InnoDB的索引文件和数据文件是在一起的，是.ibd数据文件，而MyISAM这两个则是分开的，.myd是表数据文件，.myi是索引文件

leader：嗯，回答的还算比较不错

我：（心里：tui，这还比较不错，这是没词用了吧）嗯，领导说的是，我还需要努力，有些地方还是没太搞懂呢。。。

leader：那么既然把聚集索引和非聚集索引都说出来了，那么，你再说说什么叫索引覆盖，回表，索引下推吧

# 索引覆盖，回表，索引下推

## 索引覆盖

关于索引覆盖，意思就是，只需要在一棵索引树上就能查询出来所有要查询出的数据，不需要回表，那么这就是覆盖索引。

这里简单举例说明一下 ![img](https://upyun-cdn.mistill.com/img/post_img/db10068be4c14054a5fe7571d74f60e3~tplv-k3u1fbpfcp-watermark.image) 一个表两条数据，userID，userName，age三个字段

userID是主键索引，这里创建一个复合索引

```sql
ALTER TABLE user ADD INDEX idname (userID, userName);
复制代码
```

这里我们查询一下userID和userName

```sql
EXPLAIN select userID,userName from user where userName='张三'
复制代码
```

![img](https://upyun-cdn.mistill.com/img/post_img/a97a6384ed564fc888431f209f7ba096~tplv-k3u1fbpfcp-watermark.image) 大家看一下执行计划，extra那一列有一个using index，意思是索引覆盖。

如果多加上其他字段，在查询就没有using index这个字段了

那么，什么叫回表呢？ 回表简单来说就是比如上面的userName='张三'，他是先从userName的索引树通过张三找到张三这个值对应的id，在通过id去聚集索引树上找当前数据，这个叫回表。

## 索引下推

索引下推简称ICP，是在MySQL5.6推出的

简单来说，使用ICP的话，如果是where判断中，比如where userName='张三' and age = '18' 会把userName和age都先进行判断，如果不使用ICP的话，只会先判断userName='张三'而忽略age，因为name可能会出现重复的，这个时候，假如有两个张三，但是年龄不同，就会把这两个张三都找出来，去主键索引树查询，一次一次的做回表操作，性能会有所下降。

假如：select id,userName,age from user where userName like '张%' and age = '22' 还是上面的表但是多几个字段，userName和age是一个索引树上 ![img](https://upyun-cdn.mistill.com/img/post_img/08fcf9cf2b32411a8a8f6bb838eaf115~tplv-k3u1fbpfcp-watermark.image)![img](https://upyun-cdn.mistill.com/img/post_img/dc4214f8be874c70bbdf8989000e54ec~tplv-k3u1fbpfcp-watermark.image) 表中有两个姓张的，如果不开启ICP的话，想象一下，他会先从userName和age这个索引树上，根据userName like '张%'来找到age22和23这两条数据的id，然后通过这两个id，去聚集索引树上，一次次回表查询，所以这里是需要进行两次回表，对吧。

那如果开启ICP呢？他会把userName和age都进行判断，这个时候通过userName找到两个姓张的，在判断age的话，年龄只有一个符合的，所以这个时候在根据id去回表查询，这里的话，也就是说只进行了一次回表，减少了一次呢？如果姓张的是几百个几千个呢？大家可以想象的到性能提高多少了吧。

所以，索引下推有什么好处：

- 索引下推是在非主键索引上的优化，可以有效的减少回表的次数，大大提升了查询的性能。
- 如果想关闭索引下推的话：　set optimizer_switch='index_condition_pushdown=off';

leader：小伙子可以啊，这都让你答出来了。

我：嘿嘿，也就一般吧，毕竟谁让我这么优秀呢对吧。

leader：夸夸你就飘得不行了？？？，行奥，我回去好好想想，下次再问问你，让你吃瘪。你等着小伙

我：不慌不忙，来日方长，展翅翱翔，做气质流氓，我等您！

PS：下次讲一下怎么进行sql优化好了，大家记得收藏一下