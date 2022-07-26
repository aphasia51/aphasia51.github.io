# Gin框架与Radix-Tree


Gin框架与Radix Tree

<!--more-->

## Trie

字典树，前缀树。是一种有序多叉树结构，利用字符串的公共前缀来减少查询的时间。

- 根节点不包含字符(目的是能包括所有字符串)，其余每个节点都只包含一个字符。
- 每个节点的子节点字符不同，保证唯一性。

![image-20220623105051775](https://cdn.jsdelivr.net/gh/aphasia51/images@main/blog/imagestrie.png)

## Radix Tree

前缀压缩树，优化了Trie的空间。如果树中某个父节点的子节点唯一，那么其子节点将与父节点合并，即一个节点可以包含多个字符串。

![image-20220623111554740](https://cdn.jsdelivr.net/gh/aphasia51/images@main/blog/imagesradix_tree.png)

假定我们有如下的路由注册信息:

```go
	r := gin.Default()

	r.GET("/", function1)
	r.GET("/php/", function2)
	r.GET("/python/", function3)
	r.GET("/article/", function4)
	r.GET("/article/:id/", function5)
	r.GET("/social/", function6)
	r.GET("/social/github", function6)
```

那么就可以得到一个`GET`方法对应的路由树。<br>

与`hash map`不同，以上的这种树结构还允许使用例如`:id`这样的动态部分，因为实际上是根据路由参数进行匹配。<br>

路由器为每一个请求方法管理一颗单独的树，这样比每个节点都保存一个`hash map`更节省空间。


