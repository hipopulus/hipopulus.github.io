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

* 结构体属于值类型，类属于引用类型。值类型的变量或常量传递的是它的copy，引用类型传递的是它的引用。值类型里可以定义引用类型的属性，该引用类型的属性传递的仍然是它的引用，当然这种结构在应用上是不合理的，值类型包含的属性应该同样是值类型：
        
        class SimpleClass {
            var description = "This is a simple class"
        } 

        struct SimpleStruct {
            var description = "This is a simple structure"
            var c = SimpleClass()
        }  

        var struct1 = SimpleStruct()
        var struct2 = struct1

        struct1.description = "Changed"
        struct1.c.description = "Changed"

        println(struct2.description)
        println(struct2.c.description)

* let表示声明一个常量，常量在初始化之后，不可以再被修改。如果let声明了一个引用类型的常量，表示它不可以被重新引用一个实例，但是实例所包含的属性变量是可以被修改的：

        class Person {
            var name = ""
            init(name: String) {
                self.name = name
            }
        }

        let person = Person(name: "Lisa")
        person.name = "Jacky"

* Objectiv-C只可以在class中定义类方法，而Swift的类、结构体、枚举类型里都可以定义类方法，在func前面添加static关键声明，class类型中也可以用class关键声明，它的子类可以重写class修饰的父类方法

        struct Point {
            static func moveBy(x: Int, y: Int) {}
        }

        enum SimpleEnum {
            case One, Two, Three
            static func doSomething() {}
        }

        class SimpleClass {
            static func test() {}
            class func doSomething() {}
        }

        class SubClass: SimpleClass {
            override func doSomething() {}
        }
        
* 结构体类型会自动生成初始化器：

        struct Size {
            var width: Float
            var height: Float
        }

        var big = Size(width: 5.0, height: 5.0)

* 但是如果我们为它添加了自定义的初始化器，我们将失去自动生成的初始化器：

        struct Size {
            var width: Float
            var height: Float

            init(width: Float) {
                self.width = width
                self.height = width
            }
        }

        var big = Size(width: 5.0, height: 5.0) // error

* 可以通过extension手动添加原来的初始化器，使它重新有效：

        extension Size {
            init(width: Float, height: Float) {
                self.width = width
                self.height = height
            }
        }

* 一个class、structure或enumeration的访问域可以和它们所遵守的protocol多访问域不同，但是它们实现的成员方法、变量和常量的访问域不能小于protocol的访问域，否则可能出现问题，例如在protocol级别的访问域内实现了对某class实例的type cast，却可能无法访问protocol对应的某个方法。

        internal protocol SimpleProtocl {
            func doSomthing()
        }

        private class ClassA: SimpleProtocl {
            func doSomthing() {}
        }

        public class ClassB: SimpleProtocl {
            func doSomthing() {}
        }

        internal class ClassC: SimpleProtocl {
            private func doSomthing() {} // error
        }

* 子类的访问域级别不能大于父类的访问域级别，但是子类的override成员的访问域级别不能小于对应的父类的成员访问域级别：

        class Animal {
            private func sleep() {}
            func move() {}
        }

        class Dog: Animal {
            override func sleep() {}
            private override func move() {} // error
        }

*******************************