---
layout: post
category: "Swift"
title: "while loop在swift2中的语法"
tags: ["Swift"]
---

昨天WWDC大会发布了swift2，其中一个更新是关于while loop的

原来语法是：

    var m = 2
    do {
        m = m * 2
    } while m < 100
    print(m)

更新后：

    var m = 2
    repeat {
        m = m * 2
    } while m < 100
    print(m)


*******************************