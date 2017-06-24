# You dont' know javascript笔记之什么是作用域

## 编译原理

```js
var a = 2;
```

传统编译语言编译时分3步走：

1. Tokening/Lexing

    Tokening: 把字符串拆分为有意义的子字符串。比如 var、a、 =、 2、 ;。通常就用空格来进行拆分，个人认为某些对缩进有要求的语言，在进行tokening的过程应该是比较耗费性能的，因为还要算空格的个数，所以JS对缩进没有要求。

    Lexing: Lexing和Tokening有点像，但区别在于如果拆分时要考虑a是一个单独的token还是另外一个token的一部分，就是lexing。（这里我还不太明白什么意思。。。先mark）

2. Parsing:

    把第一步得到的stream或者数组组装成一个树的过程，这棵树就叫做AST(Abstract Syntax Tree抽象语法树)。比如
    ```js 
    var a = 2;
    ```
    就可能组装成一个根节点VariableDeclaration，然后有两个子节点，分别是Identifier和AssignmentExpression, 其中AssignmentExpression又包含子节点NumericLiteral。

    ![image](https://user-images.githubusercontent.com/8369212/27505221-1f066de0-58cd-11e7-8d7b-a5e8b6091957.png)

3. Code-generation

  生成代码，这里的细节的很多了，但是书中没有展开。就是把AST生成可执行的代码，有可能是汇编？


  LHS和RHS

        LHS: left hand side look up
        RHS: right hand side look up
按我个人的理解，赋值操作都是LHS，直接使用某个变量都是RHS
```js
function foo(a) {
    var b = a;
    return a + b;
}
var c = foo(2);
```
这段代码里，LHS有3次（2次赋值，一次函数传参），RHS4次（使用foo， 使用a，使用a， 使用b）