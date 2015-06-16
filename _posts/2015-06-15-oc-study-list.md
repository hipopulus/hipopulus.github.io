---
layout: post
category: "Objective-C"
title: "Objective-C学习备忘－需要研究的问题"
tags: ["Objective-C"]
---

* ###下面的`|`符号是什么意思？

        static NSStringCompareOptions comparisonOptions = NSCaseInsensitiveSearch | NSNumericSearch | NSWidthInsensitiveSearch | NSForcedOrderingSearch;

    >   参考：<http://nshipster.com/ns_enum-ns_options/>

* ###CoreFoundation的CFAvailability.h文件中关于`CF_ENUM`和`CF_OPTIONS`的宏定义的语法如何理解：

        #if (__cplusplus && __cplusplus >= 201103L && (__has_extension(cxx_strong_enums) || __has_feature(objc_fixed_enum))) || (!__cplusplus && __has_feature(objc_fixed_enum))
        #define CF_ENUM(_type, _name) enum _name : _type _name; enum _name : _type
        #if (__cplusplus)
        #define CF_OPTIONS(_type, _name) _type _name; enum : _type
        #else
        #define CF_OPTIONS(_type, _name) enum _name : _type _name; enum _name : _type
        #endif
        #else
        #define CF_ENUM(_type, _name) _type _name; enum
        #define CF_OPTIONS(_type, _name) _type _name; enum
        #endif
    
    >   问题已解决，下面是思考过程：
*************
    >   例如，要定义一个包含四个季节的枚举常量，先从标准C的定义开始：

    >       typedef enum Season : NSInteger Season;
    >       enum Season : NSInteger { Spring, Summer, Autumn, Winter };

    >   测试：

    >       Season a = Autumn;
    >       NSLog(@"%ld", a);

    >   打印结果为：2
***********
    >   接下来，用宏定义重写：
 
    >       #define SeasonList(_season, _type) enum _season : _type _season; enum _season : _type
    >       typedef SeasonList(Season, NSUInteger) { Spring, Summer, Autumn, Winter };

    >   测试：

    >       Season a = Autumn;
    >       NSLog(@"%ld", a);

    >   打印结果为：2，和上面的标准定义的结果相同。

*******************************