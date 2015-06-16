---
layout: post
category: "Swift"
title: "Swift学习备忘－需要研究的问题"
tags: ["Swift"]
---

* HeaderDoc:[1][]-[2][]-[3][]
[1]: https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/HeaderDoc/intro/intro.html#//apple_ref/doc/uid/TP40001215-CH345-SW1
[2]: http://nshipster.com/swift-documentation/
[3]: http://nshipster.com/documentation/

* Optional类型

        var aString:String? = "Hello!"
        var aString:Optional<String> = "Hello"

* [Swift Literal Convertibles][4]
[4]: http://nshipster.com/swift-literal-convertible/?utm_source=tuicool

* Foundation框架是否用Swift重写了？

* enum实现protocol的方法

* enum的raw-value的类型需要遵循literal convertible协议

* 为什么class的成员方法可以修改成员变量的值，而值类型的成员方法[不可以][5]修改成员变量的值，除非在func前添加`mutating`修饰符？
[5]: https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Methods.html

* @objc的意义和用法

* 关于protocol的extension，增加了约束条件（`where`）和默认实现。如果针对统一个方法和属性有多个extension，应该怎么办？

*******************************