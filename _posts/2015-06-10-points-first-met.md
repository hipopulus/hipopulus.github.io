---
layout: post
category: "Swift"
title: "首次遇到的知识点"
tags: ["Swift"]
---

* `var aString: String! = "Hello, World!"`

* Error handling

* Assertion

* `===` 和 `!==` 用来比较两个**class的实例的引用**是否相同 

*  `??`用来为Optional实例解包，`a ?? b` 等效于 `if a != nil ? a! : b`

* Swift中的字符类型为`Character`，声明时需注明数据类型，否则编译器会把它当作String处理：

        var aCharacter: Character = "A"

* Unicode在String和Character中的语法是`\{n}`，n代表1个16进制的Unicode码：
    
        var aString = "\u{41}\u{42}\u{43}"
        var aCharacer: Character = "\u{41}"

* 有些字符是可以组合，形成新的字符，并且新组成的字符的长度仍然是1：

        var aCharacer: Character = "\u{65}\u{301}"

* 由于Swift的更新，获取一个String实例的字符数量的方法需要验证，官方文档说是String不在遵循`CollectionType`协议，今后需要采用最后一种方法：
        
        var aString = "Swift"
        var stringCount = countElements(aString)
        var stringCount = count(aString)
        var stringCount = aString.characters.count        

*******************************