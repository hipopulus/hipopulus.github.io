---
layout: post
category: "Swift"
title: "Swift中closure语法可以更精简"
tags: ["Closure"]
---

在Swift中调用数组的sorted方法进行排序时，需要传递一个函数类型的参数：

    func sorted(isOrderedBefore: (T, T) -> Bool) -> [T]

这个函数就是我们为数组排序定义的规则，以一个整数的数组为例：
    
    var numbers = [1, 19, 7, 12, 9, 30, 22]

我们定义一个函数，并将其作为参数调用sorted方法：

    func compare(num1: Int, num2: Int) -> Bool {
        return num1 > num2
    }

    var nums5 = numbers.sorted(compare)

    println(nums5)

结果为：`[30, 22, 19, 12, 9, 7, 1]`

如果将参数改为闭包：

    numbers.sorted({(num1: Int, num2: Int) -> Bool in return num1 > num2})

由于闭包的参数类型和返回值类型是有sorted方法确定了的，所以可以省略

    numbers.sorted({ (num1, num2) in return num1 > num2 })

参数个数也是确定的，也可以省略，并用$0、$1代替：

    numbers.sorted({ return $0 > $1 })

return也可以省略：

    numbers.sorted({ $0 > $1 })

最精简的结果是：可以用一行并且最少的代码完成排序！

*************

自定义的带函数参数的方法，同样适用：

    func sort(list: [Int], #condition: ((Int, Int) -> Bool)) -> [Int] {
        var result = [Int]()
        result.append(list.first!)
        for i in 1..<list.count {
            for j in 0..<result.count {
                if condition(list[i], result[j]) {
                    result.insert(list[i], atIndex: j)
                    break
                }
                if j == list.count - 1 {
                    result.append(list[i])
                }
            }
        }
        return result
    }

    sort(numbers) { $0 > $1 }


*******************************