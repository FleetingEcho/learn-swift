# Learn Swift

```swift
// 导入一个模块
import Foundation

// 单行注释以 // 开头
// 多行注释以 /* 开头，以 */ 结尾
/* 嵌套的多行注释
 /* 是 */
 允许的
 */

// Xcode 支持用标记注释代码，并在跳转栏中列出它们
// MARK: 分区标记
// MARK: - 带有分隔线的分区标记
// TODO: 尽快处理某事
// FIXME: 修复这段代码

// MARK: 你好，世界
// 从 Swift 3 开始，要打印内容，只需使用 `print` 方法。
// 它会自动添加换行符。
print("Hello,world!")

//
// MARK: - 变量
//

// 使用 `let` 来声明常量，使用 `var` 来声明变量。
let theAnswer = 42
var theQuestion = "What is the Answer?"
theQuestion = "How many roads must a man walk down?"
theQuestion = "What is six by nine?"
// 尝试重新分配常量会引发编译时错误
//theAnswer = 54

// 变量和常量都可以在赋值之前声明，
//   但必须在使用之前给它们赋值
let someConstant: Int
var someVariable: String
// 下面的行会引发错误：
//print(someConstant)
//print(someVariable)
someConstant = 0
someVariable = "0"
// 现在这些行是有效的：
print(someConstant)
print(someVariable)

// 如上所示，变量类型会自动推断。
//   要显式声明类型，请在变量名后写上类型，
//   用冒号分隔。
let aString: String = "A string"
let aDouble: Double = 0

// 值从不会隐式转换为另一种类型。
// 显式地创建所需类型的实例。
let stringWithDouble = aString + String(aDouble)
let intFromDouble = Int(aDouble)

// 对于字符串，使用字符串插值
let descriptionString = "The value of aDouble is \(aDouble)"
// 您可以在字符串插值中放入任何表达式。
let equation = "Six by nine is \(6 * 9), not 42!"
// 为了避免转义双引号和反斜杠，请更改字符串分隔符
let explanationString = #"The string I used was "The value of aDouble is \(aDouble)" and the result was \#(descriptionString)"#
// 可以在开始引号之前放置任意数量的井号，
//   只需在结束引号处匹配它们。 它们还将转义字符更改为后跟相同数量的井号。

let multiLineString = """
    This is a multi-line string.
    It's called that because it takes up multiple lines (wow!)
        Any indentation beyond the closing quotation marks is kept, the rest is discarded.
    You can include " or "" in multi-line strings because the delimiter is three "s.
    """

// 数组
let shoppingList = ["catfish", "water", "tulips"] // 允许在最后一个元素后面加逗号
let secondElement = shoppingList[1] // 数组是 0 索引的

// 使用 let 声明的数组是不可变的；以下行会引发编译时错误
//shoppingList[2] = "mango"

// 数组是结构体（稍后会介绍更多），因此这将创建一个副本而不是引用相同的对象
var mutableShoppingList = shoppingList
mutableShoppingList[2] = "mango"

// == 是相等运算符
shoppingList == mutableShoppingList // false

// 使用 let 声明的字典也是不可变的
var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic"
]
occupations["Jayne"] = "Public Relations"
// 字典也是结构体，所以这也会创建一个副本
let immutableOccupations = occupations

immutableOccupations == occupations // true

// 随着您添加元素，数组和字典都会自动增长
mutableShoppingList.append("blue paint")
occupations["Tim"] = "CEO"

// 它们都可以设置为空

mutableShoppingList = []
occupations = [:]

let emptyArray = [String]()
let emptyArray2 = Array<String>() // 与上面相同
// [T] 是 Array<T> 的简写
let emptyArray3: [String] = [] // 显式声明类型允许将其设置为空数组
let emptyArray4: Array<String> = [] // 与上面相同

// [Key: Value] 是 Dictionary<Key, Value> 的简写
let emptyDictionary = [String: Double]()
let emptyDictionary2 = Dictionary<String, Double>() // 与上面相同
var emptyMutableDictionary: [String: Double] = [:]
var explicitEmptyMutableDictionary: Dictionary<String, Double> = [:] // 与上面相同

// MARK: 其他变量
let øπΩ = "value" // Unicode 变量名
let 🤯 = "wow" // 表情符号变量名

// 关键字可以用作变量名
// 这些是上下文关键字，现在不会使用，因此允许使用
let convenience = "keyword"
let weak = "another keyword"
let override = "another keyword"

// 使用反引号使关键字可以作为变量名使用，即使通常不允许
let `class` = "keyword"

// MARK: - 可选值

/*
 可选值是 Swift 语言的一个特性，它们可以包含一个值，
 或包含 nil（没有值）以指示缺少值。
 nil 大致相当于其他语言中的 `null`。
 在类型之后加上问号（?）将该值标记为该类型的可选值。

 如果类型不是可选的，则保证有一个值。

 因为 Swift 要求每个属性都有一个类型，即使是 nil 也必须
 明确存储为 Optional 值。

 Optional<T> 是一个枚举，有 .none（nil）和 .some(T)（值）两种情况
 */

var someOptionalString: String? = "optional" // 可以是 nil
// T? 是 Optional<T> 的简写 — ? 是后缀操作符（语法糖）
let someOptionalString2: Optional<String> = nil
let someOptionalString3 = String?.some("optional") // 与第一个相同
let someOptionalString4 = String?.none //nil

/*
 要访问具有值的可选值的值，请使用后缀
 操作符 !，它会强制解包它。强制解包类似于说，“我
 知道这个可选值肯定有一个值，请给我。”

 尝试使用 ! 访问不存在的可选值会触发一个
 运行时错误。在使用 ! 强制解包其值之前，始终确保可选值
 包含非 nil 值。
 */

if someOptionalString != nil {
    // 我不是 nil
    if someOptionalString!.hasPrefix("opt") {
        print("有前缀")
    }
}

// Swift 支持“可选链”，这意味着您可以调用函数
//   或获取可选值的属性，它们是相应类型的可选值。
// 甚至可以多次这样做，因此称为“链式调用”。

let empty = someOptionalString?.isEmpty // Bool?

// if-let 结构 -
// if-let 是 Swift 中的一个特殊结构，允许您检查 Optional 右侧是否包含一个值，并且如果包含，则将其解包并分配给左侧。

if let someNonOptionalStringConstant = someOptionalString {
    // 有 `Some` 值，非 nil
    // someOptionalStringConstant 的类型是 String，而不是 String?
    if !someNonOptionalStringConstant.hasPrefix("ok") {
        // 没有前缀
    }
}

//if-var 也是允许的！
if var someNonOptionalString = someOptionalString {
    someNonOptionalString = "非可选且可变"
    print(someNonOptionalString)
}

// 您可以在一个 if-let 语句中绑定多个可选值。
// 如果任何绑定值为 nil，则 if 语句不执行。
if let first = someOptionalString, let second = someOptionalString2,
    let third = someOptionalString3, let fourth = someOptionalString4 {
    print("\(first), \(second), \(third), and \(fourth) are all not nil")
}

//if-let 支持“,”（逗号）子句，用于对新绑定的可选值施加条件。
// 赋值和“,” 子句都必须通过。
let someNumber: Int? = 7
if let num = someNumber, num > 3 {
    print("num is not nil and is greater than 3")
}

// 隐式解包可选值 —— 一个不需要解包的可选值
let unwrappedString: String! = "期望值。"

// 这里是区别：
let forcedString = someOptionalString! // 需要感叹号
let implicitString = unwrappedString // 不需要感叹号

/*
您可以将隐式解包的可选值视为在使用时自动解包可选值的许可。
与每次使用可选名称后面放置感叹号不同，
在声明时，每次使用可选的类型后面放置感叹号。
*/

// 否则，您可以像对待普通可选值一样对待隐式解包的可选值
//（即，if-let、!= nil 等）

// 在 Swift 5 之前，T! 是 ImplicitlyUnwrappedOptional<T> 的简写
// 在 Swift 5 及更高版本中，使用 ImplicitlyUnwrappedOptional 会引发编译时错误。
//var unwrappedString2: ImplicitlyUnwrappedOptional<String> = "Value is expected." //error

// 空合并运算符 ?? 如果可选值包含非 nil 值，则解包，否则返回默认值。
someOptionalString = nil
let someString = someOptionalString ?? "abc"
print(someString) // abc
// a ?? b 是 a != nil ? a! : b 的简写

// MARK: - 控制流

let condition = true
if condition { print("condition is true") } // 不能省略大括号

if theAnswer > 50 {
    print("theAnswer > 50")
} else if condition {
    print("condition is true")
} else {
    print("Neither are true")
}

// `if` 语句中的条件必须是 `Bool`，因此以下代码是错误的，不是对零的隐式比较
//if 5 {
//    print("5 is not zero")
//}

// Switch
// 必须是穷尽的
// 不会隐式地贯穿，使用 fallthrough 关键字
// 非常强大，像带有语法糖的 `if` 语句
// 它们支持 String、对象实例和基本类型（Int、Double 等）
let vegetable = "red pepper"
let vegetableComment: String
switch vegetable {
case "celery":
    vegetableComment = "加点葡萄干，做成蚂蚁上树。"
case "cucumber", "watercress": // 匹配多个值
    vegetableComment = "那会是个好茶三明治。"
case let localScopeValue where localScopeValue.hasSuffix("pepper"):
    vegetableComment = "是辣的 \(localScopeValue) 吗？"
default: // 必须的（为了覆盖所有可能的输入）
    vegetableComment = "在汤里所有东西都好吃。"
}
print(vegetableComment)

// 使用 `for-in` 循环遍历序列，例如数组、字典、范围等。
for element in shoppingList {
    print(element) // shoppingList 的类型是 `[String]`，所以 element 的类型是 `String`
}
// 遍历字典不保证任何特定顺序
for (person, job) in immutableOccupations {
    print("\(person)'s job is \(job)")
}
for i in 1...5 {
    print(i, terminator: " ") // 打印 "1 2 3 4 5"
}
for i in 0..<5 {
    print(i, terminator: " ") // 打印 "0 1 2 3 4"
}
// 使用 range 的 for-in 循环可以替代 C 风格的 for 循环：
//    for (int i = 0; i < 10; i++) {
//        //代码
//    }
// 变成：
//    for i in 0..<10 {
//        //代码
//    }
// 要以步长大于一的方式遍历，可以使用 stride(from:to:by:) 或 stride(from:through:by) 函数
//`for i in stride(from: 0, to: 10, by: 2)` 等同于 `for (int i = 0; i < 10; i += 2)`
//`for i in stride(from: 0, through: 10, by: 2)` 等同于 `for (int i = 0; i <= 10; i += 2)

// while 循环与大多数语言相同
var i = 0
while i < 5 {
    i += Bool.random() ? 1 : 0
    print(i)
}

// 这类似于其他语言中的 do-while 循环 - 循环的主体至少执行一次
repeat {
    i -= 1
    i += Int.random(in: 0...3)
} while i < 5

// continue 语句在下一次迭代时继续执行循环
// break 语句立即结束循环

// MARK: - 函数

// 函数是一种一等公民类型，这意味着它们可以嵌套在函数中，并且可以传递。
// 具有 Swift 标头文档的函数（格式为 Swift 修改的 Markdown 语法）

/// 问候操作。
///
/// - Parameters:
///   - name: 一个名称。
///   - day: 一天。
/// - Returns: 包含名称和天值的字符串。
func greet(name: String, day: String) -> String {
    return "Hello \(name), today is \(day)."
}
greet(name: "Bob", day: "Tuesday")

// 理想情况下，函数名称和参数标签组合成函数调用，类似于句子。
func sayHello(to name: String, onDay day: String) -> String {
    return "Hello \(name), the day is \(day)"
}
sayHello(to: "John", onDay: "Sunday")

// 不返回任何内容的函数可以省略返回箭头；它们不需要声明它们返回 Void（尽管可以）。
func helloWorld() {
    print("Hello, World!")
}

// 参数标签可以为空
func say(_ message: String) {
    print(#"I say "\#(message)""#)
}
say("Hello")

// 调用函数时可以省略默认参数。
func printParameters(requiredParameter r: Int, optionalParameter o: Int = 10) {
    print("The required parameter was \(r) and the optional parameter was \(o)")
}
printParameters(requiredParameter: 3)
printParameters(requiredParameter: 3, optionalParameter: 6)

// 可变参数 - 每个函数只能有一个可变参数集。
func setup(numbers: Int...) {
    // 它是一个数组
    let _ = numbers[0]
    let _ = numbers.count
}

// 通过引用传递
func swapTwoInts(a: inout Int, b: inout Int) {
    let tempA = a
    a = b
    b = tempA
}
var someIntA = 7
var someIntB = 3
swapTwoInts(a: &someIntA, b: &someIntB) // 变量名前必须带上 &
print(someIntB) // 7

type(of: greet) // (String, String) -> String
type(of: helloWorld) // () -> Void

// 传递和返回函数
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)

func performFunction(_ function: (String, String) -> String, on string1: String, and string2: String) {
    let result = function(string1, string2)
    print("The result of calling the function on \(string1) and \(string2) was \(result)")
}

// 函数返回多个项目的元组
func getGasPrices() -> (Double, Double, Double) {
    return (3.59, 3.69, 3.79)
}
let pricesTuple = getGasPrices()
let price = pricesTuple.2 // 3.79
// 使用 _（下划线）忽略元组（或其他）值
let (_, price1, _) = pricesTuple // price1 == 3.69
print(price1 == pricesTuple.1) // true
print("Gas price: \(price)")

// 带标签/命名的元组参数
func getGasPrices2() -> (lowestPrice: Double, highestPrice: Double, midPrice: Double) {
    return (1.77, 37.70, 7.37)
}
let pricesTuple2 = getGasPrices2()
let price2 = pricesTuple2.lowestPrice
let (_, price3, _) = pricesTuple2
print(pricesTuple2.highestPrice == pricesTuple2.1) // true
print("Highest gas price: \(pricesTuple2.highestPrice)")

// guard 语句
func testGuard() {
    // guard 语句提供了提前退出或中断的机制，将错误处理代码放在条件附近。
    // 它将它声明的变量放在与 guard 语句相同的范围内。
    // 它们使得更容易避免“金字塔式的地狱”。
    guard let aNumber = Optional<Int>(7) else {
        return // guard 语句必须退出它们所在的作用域。
        // 通常使用 `return` 或 `throw`。
    }

    print("number is \(aNumber)")
}

testGuard()

// 请注意，print 函数声明如下：
//     func print(_ input: Any..., separator: String = " ", terminator: String = "\n")
// 若要不打印换行符：
print("没有换行", terminator: "")
print("!")

// MARK: - 闭包

var numbers = [1, 2, 6]

// 函数是闭包的特殊情况（{}）

// 闭包示例。
// `->` 分隔参数和返回类型
// `in` 将闭包头部与闭包体分开
numbers.map({
    (number: Int) -> Int in
    let result = 3 * number
    return result
})

// 当类型已知时，我们可以这样做
numbers = numbers.map({ number in 3 * number })
// 甚至这样
//numbers = numbers.map({ $0 * 3 })

print(numbers) // [3, 6, 18]

// 尾随闭包
numbers = numbers.sorted { $0 > $1 }

print(numbers) // [18, 6, 3]

// MARK: - 枚举

// 枚举可以选择是特定类型的，也可以是独立的。
// 它们可以包含像类一样的方法。

enum Suit {
    case spades, hearts, diamonds, clubs
    var icon: Character {
        switch self {
        case .spades:
            return "♤"
        case .hearts:
            return "♡"
        case .diamonds:
            return "♢"
        case .clubs:
            return "♧"
        }
    }
}

// 枚举值允许简写语法，在显式声明变量时不需要输入枚举类型
var suitValue: Suit = .hearts

// 符合 CaseIterable 协议会自动生成 allCases 属性，
//   包含所有值。它适用于没有关联值或 @available 属性的枚举。
enum Rank: CaseIterable {
    case ace
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
    var icon: String {
        switch self {
        case .ace:
            return "A"
        case .two:
            return "2"
        case .three:
            return "3"
        case .four:
            return "4"
        case .five:
            return "5"
        case .six:
            return "6"
        case .seven:
            return "7"
        case .eight:
            return "8"
        case .nine:
            return "9"
        case .ten:
            return "10"
        case .jack:
            return "J"
        case .queen:
            return "Q"
        case .king:
            return "K"
        }
    }
}

for suit in [Suit.clubs, .diamonds, .hearts, .spades] {
    for rank in Rank.allCases {
        print("\(rank.icon)\(suit.icon)")
    }
}

// 字符串枚举可以直接设置原始值
// 或者它们的原始值将从枚举字段派生
enum BookName: String {
    case john
    case luke = "Luke"
}
print("Name: \(BookName.john.rawValue)")

// 具有关联值的枚举
enum Furniture {
    // 与 Int 关联
    case desk(height: Int)
    // 与 String 和 Int 关联
    case chair(String, Int)

    func description() -> String {
        // let 的放置位置都可以接受
        switch self {
        case .desk(let height):
            return "高度 \(height) 厘米的桌子"
        case let .chair(brand, height):
            return "高度 \(height) 厘米的 \(brand) 椅子"
        }
    }
}

var desk: Furniture = .desk(height: 80)
print(desk.description())     // "Desk with 80 cm"
var chair = Furniture.chair("Foo", 40)
print(chair.description())    // "Chair of Foo with 40 cm"

// MARK: - 结构体 & 类

/*
 Swift 中的结构体和类有许多共同点。两者都可以：
 - 定义属性以存储值
 - 定义方法以提供功能
 - 定义下标以使用下标语法访问它们的值
 - 定义初始化器以设置它们的初始状态
 - 可以扩展以扩展其功能超出默认实现
 - 符合协议以提供某种类型的标准功能

 类具有结构体没有的附加功能：
 - 继承使一个类能够继承另一个类的特性。
 - 类型转换使您能够在运行时检查和解释类实例的类型。
 - 反初始化器使类的实例能够释放其分配的任何资源。
 - 引用计数允许对类实例进行多个引用。

 除非需要出于这些原因之一使用类，否则请使用结构体。

 结构体是值类型，而类是引用类型。
 */

// MARK: 结构体

struct NamesTable {
    let names: [String]

    // 自定义下标
    subscript(index: Int) -> String {
        return names[index]
    }
}

// 结构体具有自动生成的（隐式）指定的“成员初始化器”
let namesTable = NamesTable(names: ["我", "他们"])
let name = namesTable[1]
print("Name is \(name)") // Name is Them

// MARK: 类

class Shape {
    func getArea() -> Int {
        return 0
    }
}

class Rect: Shape {
    var sideLength: Int = 1

    // 自定义 getter 和 setter 属性
    var perimeter: Int {
        get {
            return 4 * sideLength
        }
        set {
            // `newValue` 是 setter 可用的隐式变量
            sideLength = newValue / 4
        }
    }

    // 计算属性必须声明为 `var`，你知道的，因为它们可以改变
    var smallestSideLength: Int {
        return self.sideLength - 1
    }
}

    // 惰性加载属性
    // subShape 保持 nil（未初始化）直到调用 getter 方法
    lazy var subShape = Rect(sideLength: 4)

    // 如果您不需要自定义 getter 和 setter，
    // 但仍希望在获取或设置属性之前和之后运行代码，
    // 您可以使用 `willSet` 和 `didSet`
    var identifier: String = "defaultID" {
        // `someIdentifier` 参数将是新值的变量名
        willSet(someIdentifier) {
            print(someIdentifier)
        }
    }

    init(sideLength: Int) {
        self.sideLength = sideLength
        // 总是在初始化自定义属性时最后调用 super.init()
        super.init()
    }

    func shrink() {
        if sideLength > 0 {
            sideLength -= 1
        }
    }

    override func getArea() -> Int {
        return sideLength * sideLength
    }
}

// 一个简单的 `Square` 类扩展了 `Rect`
class Square: Rect {
    // 使用方便的初始化器可以使调用指定的初始化器更快、更“方便”。
    // 方便的初始化器调用同一类中的其他初始化器，并向一个或多个参数传递默认值。
    // 方便的初始化器也可以有参数，这对于自定义调用的初始化器参数或基于传递的值选择适当的初始化器非常有用。
    convenience init() {
        self.init(sideLength: 5)
    }
}

var mySquare = Square()
print(mySquare.getArea()) // 25
mySquare.shrink()
print(mySquare.sideLength) // 4

// 转换实例
let aShape = mySquare as Shape

// 向下转型实例：
// 由于向下转型可能失败，结果可以是可选的（as?）或隐式解包的可选的（as!）。
let anOptionalSquare = aShape as? Square // 如果 aShape 不是 Square，则返回 nil
let aSquare = aShape as! Square // 如果 aShape 不是 Square，则会抛出运行时错误

// 比较实例，不同于 == 比较对象（相等于）
if mySquare === mySquare {
    print("是的，它是 mySquare")
}

// 可选初始化
class Circle: Shape {
    var radius: Int
    override func getArea() -> Int {
        return 3 * radius * radius
    }

    // 在 `init` 后面放一个问号后缀是一个可选初始化
    // 可以返回 nil
    init?(radius: Int) {
        self.radius = radius
        super.init()

        if radius <= 0 {
            return nil
        }
    }
}

var myCircle = Circle(radius: 1)
print(myCircle?.getArea())    // Optional(3)
print(myCircle!.getArea())    // 3
var myEmptyCircle = Circle(radius: -1)
print(myEmptyCircle?.getArea())    // "nil"
if let circle = myEmptyCircle {
    // 由于 myEmptyCircle 是 nil，所以不会执行
    print("circle is not nil")
}

// MARK: - 协议

// 协议在一些其他语言中也被称为接口

// `protocol` 可以要求符合类型具有特定的
// 实例属性、实例方法、类型方法、
// 运算符和下标。

protocol ShapeGenerator {
    var enabled: Bool { get set }
    func buildShape() -> Shape
}

// MARK: - 其他

// MARK: 类型别名

// 类型别名允许通过另一个名称引用一个类型（或类型组合）
typealias Integer = Int
let myInteger: Integer = 0

// MARK: = 运算符

// 赋值不返回值。这意味着它不能用在条件语句中，
//   并且以下语句也是非法的
//    let multipleAssignment = theQuestion = "No questions asked"
//但你可以这样做：
let multipleAssignment = "No questions asked", secondConstant = "No answers given"

// MARK: 范围

// ..< 和 ... 运算符创建范围。

// ... 在两端都包含（一个“闭合范围”）- 数学上，[0, 10]
let _0to10 = 0...10
// ..< 在左边包含，右边不包含（一个“范围”）- 数学上，[0, 10)
let singleDigitNumbers = 0..<10
// 您可以省略一个端点（一个“PartialRangeFrom”）- 数学上，[0, ∞)
let toInfinityAndBeyond = 0...
// 或另一个端点（一个“PartialRangeTo”）- 数学上，(-∞, 0)
let negativeInfinityToZero = ..<0
// （一个“PartialRangeThrough”）- 数学上，(-∞, 0]
let negativeInfinityThroughZero = ...0

// MARK: 通配符运算符

// 在 Swift 中，_ (下划线) 是通配符运算符，允许忽略值

// 它允许声明函数时不带参数标签：

func function(_ labelLessParameter: Int, label labeledParameter: Int, labelAndParameterName: Int) {
    print(labelLessParameter, labeledParameter, labelAndParameterName)
}
function(0, label: 0, labelAndParameterName: 0)

// 您可以忽略函数的返回值
func printAndReturn(_ str: String) -> String {
    print(str)
    return str
}
let _ = printAndReturn("一些字符串")

// 您可以忽略元组的一部分并保留其中的一部分
func returnsTuple() -> (Int, Int) {
    return (1, 2)
}
let (_, two) = returnsTuple()

// 您可以忽略闭包参数
let closure: (Int, Int) -> String = { someInt, _ in
    return "\(someInt)"
}
closure(1, 2) // 返回 1

// 您可以忽略循环中的值
for _ in 0..<10 {
    // 要执行10次的代码
}

// MARK: 访问控制

/*
 Swift 有五个级别的访问控制:
 - Open: 可访问*和可子类化*在导入它的任何模块中。
 - Public: 在导入它的任何模块中可访问，在声明它的模块中可子类化。
 - Internal: 在声明它的模块中可访问和可子类化。
 - Fileprivate: 在声明它的文件中可访问和可子类化。
 - Private: 在封闭声明中可访问和可子类化（思考内部类/结构/枚举）

 更多信息请参阅：https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html
 */

// MARK: 防止覆盖

// 您可以在类或实例方法之前添加关键字`final`，或在属性之前添加关键字，以防止其被覆盖
class Shape {
    final var finalInteger = 10
}

// 防止类被子类化
final class ViewManager {
}

// MARK: 条件编译、编译时诊断和可用性条件

// 条件编译
#if false
print("此代码将不会被编译")
#else
print("此代码将被编译")
#endif
/*
 选项有：
 os()                   macOS、iOS、watchOS、tvOS、Linux
 arch()                 i386、x86_64、arm、arm64
 swift()                >= 或 < 后跟一个版本号
 compiler()             >= 或 < 后跟一个版本号
 canImport()            一个模块名
 targetEnvironment()    模拟器
 */
#if swift(<3)
println()
#endif

// 编译时诊断
// 您可以使用#warning(message)和#error(message)让编译器发出警告和/或错误
#warning("这将是一个编译时警告")
//  #error("这将是一个编译时错误")

// 可用性条件
if #available(iOSMac 10.15, *) {
    // macOS 10.15 可用，您可以在此处使用它
} else {
    // macOS 10.15 不可用，使用替代的 API
}

// MARK: Any 和 AnyObject

// Swift 支持存储任何类型的值。
// 为此，有两个关键字：`Any` 和 `AnyObject`
// `AnyObject` == Objective-C 中的 `id`
// `Any` 适用于任何值（类、Int、结构体等）
var anyVar: Any = 7
anyVar = "Changed value to a string, not good practice, but possible."
let anyObjectVar: AnyObject = Int(1) as NSNumber

// MARK: 扩展

// 扩展允许您为已声明的类型添加额外的功能，甚至是您没有源代码的类型。

// Square现在“遵循”`CustomStringConvertible`协议
extension Square: CustomStringConvertible {
    var description: String {
        return "面积：\(self.getArea()) - ID：\(self.identifier)"
    }
}

print("正方形：\(mySquare)")

// 您还可以扩展内置类型
extension Int {
    var doubled: Int {
        return self * 2
    }

    func multipliedBy(num: Int) -> Int {
        return num * self
    }

    mutating func multiplyBy(num: Int) {
        self *= num
    }
}

print(7.doubled) // 14
print(7.doubled.multipliedBy(num: 3)) // 42

// MARK: 泛型

// 泛型：类似于Java和C#。使用`where`关键字指定泛型的要求。

func findIndex<T: Equatable>(array: [T], valueToFind: T) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}
findIndex(array: [1, 2, 3, 4], valueToFind: 3) // Optional(2)

// 您也可以扩展带有泛型的类型
extension Array where Array.Element == Int {
    var sum: Int {
        var total = 0
        for el in self {
            total += el
        }
        return total
    }
}

// MARK: 运算符

// 自定义运算符可以以字符开始：
//      / = - + * % < > ! & | ^ . ~
// 或
// Unicode 数学、符号、箭头、装饰和线条/方框绘图字符。
prefix operator !!!

// 一个前缀运算符，当使用时会使边长增加三倍
prefix func !!! (shape: inout Square) -> Square {
    shape.sideLength *= 3
    return shape
}

// 当前值
print(mySquare.sideLength) // 4

// 使用自定义 !!! 运算符改变边长，尺寸增加3倍
!!!mySquare
print(mySquare.sideLength) // 12

// 运算符也可以是泛型的
infix operator <->
func <-><T: Equatable> (a: inout T, b: inout T) {
    let c = a
    a = b
    b = c
}

var foo: Float = 10
var bar: Float = 20

foo <-> bar
print("foo is \(foo), bar is \(bar)") // "foo is 20.0, bar is 10.0"

// MARK: - 错误处理

// 当抛出错误时，使用`Error`协议捕获
enum MyError: Error {
    case badValue(msg: String)
    case reallyBadValue(msg: String)
}

// 使用`throws`标记的函数必须使用`try`调用
func fakeFetch(value: Int) throws -> String {
    guard 7 == value else {
        throw MyError.reallyBadValue(msg: "Some really bad value")
    }

    return "test"
}
func testTryStuff() {
    // 假定不会抛出错误，否则会引发运行时异常
    let _ = try! fakeFetch(value: 7)

    // 如果抛出错误，则继续执行，但如果值为nil
    // 它还会将每个返回值包装在可选项中，即使它已经是可选的
    let _ = try? fakeFetch(value: 7)

    do {
        // 正常的尝试操作，通过`catch`块提供错误处理
        try fakeFetch(value: 1)
    } catch MyError.badValue(let msg) {
        print("错误消息：\(msg)")
    } catch {
        // 必须是穷尽的
    }
}

testTryStuff()
```