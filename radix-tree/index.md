# Gin框架与Radix-Tree


Gin框架与Radix Tree

tags: ["go", gin"]
categories: ["go", "gin"]

## Trie

字典树，前缀树。是一种有序多叉树结构，利用字符串的公共前缀来减少查询的时间。

- 根节点不包含字符(目的是能包括所有字符串)，其余每个节点都只包含一个字符。
- 每个节点的子节点字符不同，保证唯一性。

![image-20220623105051775](https://cdn.jsdelivr.net/gh/aphasia51/images@main/blog/imagestrie.png)

## Radix Tree

前缀压缩树，优化了Trie的空间。如果树中某个父节点的子节点唯一，那么其子节点将与父节点合并，即一个节点可以包含多个字符串。

![image-20220623111554740](https://cdn.jsdelivr.net/gh/aphasia51/images@main/blog/imagesradix_tree.png)




