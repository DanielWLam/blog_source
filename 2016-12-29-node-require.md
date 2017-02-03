---
title: nodejs require语法简析
---

## 参数
require(arg)

arg要么是文件名，要么是路径，如下：

```js

	var level3_1 = require('level3_1.js'); //文件.js
	var level3_2 = require('./level3_2.js'); //路径+文件.js
	var level3_3 = require('./level3_3'); //路径+文件
	var inlevel3_3 = require('./level3_3/'); //路径/
	var level3_4 = require('level3_4'); //文件
	
	level3_1(); //i am 3_1
	level3_2(); //i am 3_2
	level3_3(); //i am 3_3
	inlevel3_3; //i am 3_3 in directory
	level3_4(); //i am 3_4
```

## require(x)

1. 如果x是核心模块，直接加载
2. 如果x是以./或者/或者../开头的，则认为是路径，则先尝试当作文件加载的方式加载，找不到就按路径加载的方式加载
3. 如果直接是一个名字，则按node_modules方式加载


### 文件加载：

1. 如果X是一个文件，则直接加载X作为js文件加载；
2. 如果X.js存在，则加载x.js
3. 如果X.json存在，则把x.json的内容作为js对象加载；
4. 如果x.node存在，则把x.node作为二进制文件加载；

### 路径加载：

1. 如果X/package.json存在， 把package.json里main指向的文件加载；
2. 如果X/index.js存在，则加载X/index.js
3. 如果X/index.json存在，则把X/index.json的内容作为js对象加载；
4. 如果X/index.node存在，则以二进制文件的方式加载x.node

### node_modules加载：

从本文件所在目录开始，执行

1. 问文件加载的方式加载目录下node_moudles的X
2. 没有找到的话，就按路径加载的方式加载该目录下node_moudles的X, 直到全局NODE_MODULES