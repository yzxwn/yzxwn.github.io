## typescript

[TS Eslint规则说明](https://www.cnblogs.com/minigrasshopper/p/8064218.html)

#### 基础类型
* 字符串：string
* 数字：number
* 布尔：boolean
* 数组：boolean[]，number[]，string[]
* 元祖Tuple：表示一个已知元素数量和类型的数组，各元素的类型不必相同（例： lat a:[string, number]=['hello', 10]）
* 枚举：
```
enum Color {Red, Green, Blue} //默认enum Color {Red = 0, Green = 1, Blue = 2}
let c: Color = Color.Green;
```
* any：直接通过类型检查器
* void：表示没有任何类型，只能赋值undefined和null
* undefined/null：默认情况下null和undefined是所有类型的子类型（例： let a:number=null）
* never：表示的是那些永不存在的值的类型
```
/*
never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型；
变量也可能是 never类型，当它们被永不为真的类型保护所约束时。
never类型是任何类型的子类型，也可以赋值给任何类型；
然而，没有类型是never的子类型或可以赋值给never类型（除了never本身之外）。
即使 any也不可以赋值给never。
*/
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}
// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}
// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```
* object：表示非原始类型，也就是除number，string，boolean，symbol，null或undefined之外的类型
```
//使用object类型，就可以更好的表示像Object.create这样的API
declare function create(o: object | null): void;
create({ prop: 0 }); // OK
create(null); // OK
create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```
* 类型断言：这种方式可以告诉编译器，“相信我，我知道自己在干什么”
```
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;//“尖括号”语法
let strLength: number = (someValue as string).length;//as语法
//在TypeScript里使用JSX时，只有 as语法断言是被允许的
```
#### 变量声明
* let 、const
```
1、块作用域
2、暂时性死区（不能在被声明之前读或写）
3、不能重复声明
```
* 解构
```
1、数组解构
2、对象解构
3、属性重命名
let { a: newName1, b: newName2 } = o;
let newName1 = o.a, newName2 = o.b;
4、默认值
function keepWholeObject(wholeObject: { a: string, b?: number }) {
    let { a, b = 1001 } = wholeObject;
}
5、函数声明
function f({ a, b = 0 } = { a: "" }): void {
    // ...
}
f({ a: "yes" }); // ok, default b = 0
f(); // ok, default to {a: ""}, which then defaults b = 0
f({}); // error, 'a' is required if you supply an argument
5、展开数组/对象（仅包含对象自身的可枚举属性）（TypeScript编译器不允许展开泛型函数上的类型参数）
```
#### 接口
* interface（只要传入的对象满足上面提到的必要条件，可以包含更多属性）
```
interface LabelledValue {
  label: string;
}
function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}
let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```
* 可选属性
```
interface SquareConfig {
  color: string;
  width?: number;
}
```
* 只读属性
```
interface SquareConfig {
  color: string;
  readonly width: number;
}
```
* 数组只读：ReadonlyArray<T>
```
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error! 也不能赋值到一个已规定类型的普通数组
a = ro as number[]; //可以用类型断言重写
```
* 额外的属性检查
```
interface SquareConfig {
    color?: string;
    width?: number;
}
function createSquare(config: SquareConfig){
    // ...
}
let mySquare = createSquare({ colour: "red", width: 100 });//对象字面量会被特殊对待，如果一个对象字面量存在任何“目标类型”不包含的属性时会得到一个错误
//1、使用类型断言
let mySquare = createSquare({ width: 100, opacity: 0.5 } as SquareConfig);
//2、添加一个字符串索引签名
let squareOptions = { colour: "red", width: 100 };
let mySquare = createSquare(squareOptions);
```
* 使用接口表示函数类型
```
//函数的参数名不需要与接口里定义的名字相匹配，要求对应位置上的参数类型是兼容的
interface SearchFunc {
  (source: string, subString: string): boolean;
}
```
* 可索引的类型
```
interface SquareConfig {
  color: string;
  [index: number]: string;//当用 number去索引StringArray时会得到string类型的返回值
  [propName: string]: any;//任意数量的其它属性
}
//数字索引的返回值必须是字符串索引返回值类型的子类型
```
* 类实现接口
```
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date);
}
class Clock implements ClockInterface {
    currentTime: Date;
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
//规定构造函数类型
nterface ClockConstructor {
    new (hour: number, minute: number): ClockInterface;
}
interface ClockInterface {
    tick();
}
function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
    return new ctor(hour, minute);
}
class DigitalClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() {
        console.log("beep beep");
    }
}
class AnalogClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() {
        console.log("tick tock");
    }
}
let digital = createClock(DigitalClock, 12, 17);
let analog = createClock(AnalogClock, 7, 32);
```
* 接口继承接口（可继承多个）
```
interface Shape {
    color: string;
}
interface PenStroke {
    penWidth: number;
}
interface Square extends Shape, PenStroke {
    sideLength: number;
}
let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```
* 混合类型
```
//一个对象可以同时做为函数和对象使用
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}
function getCounter(): Counter {
    let counter = <Counter>function (start: number) { };
    counter.interval = 123;
    counter.reset = function () { };
    return counter;
}
let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```
* 接口继承类
```
//当接口继承了一个类类型时，它会继承类的成员但不包括其实现。 就好像接口声明了所有类中存在的成员，但并没有提供具体实现一样。 接口同样会继承到类的private和protected成员
class Control {
    private state: any;
}
interface SelectableControl extends Control {
    select(): void;
}
class Button extends Control implements SelectableControl {
    select() { }
}
class TextBox extends Control {
    select() { }
}
// 错误：“Image”类型缺少“state”属性。
class Image implements SelectableControl {
    select() { }
}
```
#### 类
* 继承
* 公共，私有与受保护的修饰符（public、private、protected）
* 静态属性
* 抽象类（abstract）：抽象类中的抽象方法不包含具体实现并且必须在派生类中实现
#### 函数
* 重载：为同一个函数提供多个函数类型定义来进行函数重载
#### 泛型
*使返回值的类型与传入参数的类型是相同的
```
function identity<T>(arg: T): T {
    return arg;
}
let output = identity<string>("myString");
let output = identity("myString");//类型推论
```
* 泛型函数
```
function identity<T>(arg: T): T {
    return arg;
}
let myIdentity: <T>(arg: T) => T = identity;
let myIdentity: {<T>(arg: T): T} = identity;
```
* 泛型类
```
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}
let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };
```
#### 类型兼容性
```
```
#### 高级类型
* 交叉类型：将多个类型合并为一个类型，包含了所需的所有类型的特性，用竖线（ & ）分隔每个类型
* 联合类型：表示一个值可以是几种类型之一，用竖线（ | ）分隔每个类型
* 类型别名：（对比接口，用于联合类型或元祖类型）
```
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
```
#### Symbols
```
```
#### 迭代器和生成器（for..of 、for..in ）
```
```
#### 模块
```
```
#### 命名空间
```
```
#### 命名空间和模块
```
```
#### 模块解析
```
```
#### 声明合并
```
```
#### JSX
```
```
#### 装饰器
```
```
#### Mixins
```
```
#### 三斜杆指令
```
```
#### JavaScript文件类型检查
```
```