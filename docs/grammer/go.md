### 一、类型

1、rune   int32 表示一个Unicode节点

uintptr  指针

complex128    a+bi

2、x的平方根牛顿法：假设z=1.  z-=(z*z-x)/(2*z) 

### 二、结构

3、defer

defer 语句会将函数推迟到外层函数返回之后执行。

推迟调用的函数其参数会立即求值，但直到外层函数返回前该函数都不会被调用。

多个defer时推迟的函数调用会被压入一个栈中。当外层函数返回时，被推迟的函数会按照后进先出的顺序调用。

### 三、指针

1、与 C 不同，Go 没有指针运算。

2、结构体指针

结构体字段可以通过结构体指针来访问。

如果我们有一个指向结构体的指针 `p`，那么可以通过 `(*p).X` 来访问其字段 `X`。不过这么写太啰嗦了，所以语言也允许我们使用隐式间接引用，直接写 `p.X` 就可以。

### 四、数组与切片

1、var a [10]int

a:=s[0:len(s)]

2、`make` 函数会分配一个元素为零值的数组并返回一个引用了它的切片。b := make([]int, 0, 5)

3、使用切片来创建切片其实还是使用底层数组来构建新的切片

4、

```
func append(s []T, vs ...T) []T
```

`append` 的第一个参数 `s` 是一个元素类型为 `T` 的切片，其余类型为 `T` 的值将会追加到该切片的末尾。

5、当使用 `for` 循环遍历切片时，每次迭代都会返回两个值。第一个值为当前元素的下标，第二个值为该下标所对应元素的一份副本。

```Go
a:= make([]int,10,10)
for key,value:=range a{
    fmt.printf("第%v个元素是%v",key,value)
}
```

6、切片作为参数传递时，影响原值；数组作为参数传递时，不影响原值。

### 五、映射

```go
m := make(map[keyType]valueType,size,cap)

var m = map[string]Vertex{
    "Bell Labs": {40.68433, -74.39967},
    "Google":    {37.42202, -122.08408},

    var m = map[string]Vertex{
    "Bell Labs": Vertex{
        40.68433, -74.39967,
    },
    "Google": Vertex{
        37.42202, -122.08408,
    },
      插入修改：
        m["zsy"] = 24
      获取
        age:=m["zsy"]
      删除
        delete(m,"zsy")
      双赋值检测某个key是否存在
        age,ok:=m["zsy"]  不存在 age为0 nil  ""等
```

### 六、函数

1、函数值

函数值可以作为参数和返回值

```go
hypot := func(x, y float64) float64 {
        return math.Sqrt(x*x + y*y)
}
fmt.Println(hypot(5, 12))
```

2、闭包

Go 函数可以是一个闭包。闭包是一个函数值，它引用了其函数体之外的变量。该函数可以访问并赋予其引用的变量的值，换句话说，该函数被这些变量“绑定”在一起。

```go
package main

import "fmt"
//斐波那契
// 返回一个“返回int的函数”
func fibonacci() func() int {
    sum1:=-1
    sum2:=1
    return func() int{
        test:=sum1
        sum1 = sum2
        sum2 += test
        return sum2
    }
}

func main() {
    f := fibonacci()
    for i := 0; i < 10; i++ {
        fmt.Println(f())
    }
}
```

### 七、方法和接口

1、结构体

```go
type Vertex struct {
    X, Y float64
}
```

2、接口

```go
//接口（虚基类）**接口类型** 是由一组方法签名定义的集合
//在内部，接口值可以看做包含值和具体类型的元组
//接口值为nil的时候仍然会被nil接受者的方法接收，一般底层在某个接受者的方法实现中使用接受者==nil{}来处理。注意: 保存了 nil 具体值的接口其自身并不为 nil。如果没有底层接受者保存nil接口值，那么接口值nil无法调用方法
type Abser interface {
    Abs() float64
}
```

指定了零个方法的接口值被称为 *空接口：*

```
interface{}
```

空接口可保存任何类型的值。（因为每个类型都至少实现了零个方法。）

空接口被用来处理未知类型的值。例如，`fmt.Print` 可接受类型为 `interface{}` 的任意数量的参数。

3、方法（cpp中的类函数)

```go
func (接受者对象 接受者类型)方法名（形参）返回值{}

//接收者的类型定义和方法声明必须在同一包内；不能为内建类型声明方法。下面是可以的
type MyFloat float64
//指针接收者可以修改接收者
func(f *MyFloat) Resive(){
    *f = 1.0
}

func (f MyFloat) Abs() float64 {
    if f < 0 {
        return float64(-f)
    }
    return float64(f)
}

func main() {
    f := MyFloat(-math.Sqrt2)
    fmt.Println(f.Abs())
}
```

接受一个值作为参数的函数必须接受一个指定类型的值

而以值为接收者的方法被调用时，接收者既能为值又能为指针

指针为接收者，调用必须为指针

### 八、标准库

![](D:\help\marktext-x64-win\data\2023-08-15-16-26-42-image.png)

![](D:\help\marktext-x64-win\data\2023-08-15-16-26-46-image.png)
