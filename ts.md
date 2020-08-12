# typescript编码规范

## 1. 基本格式
### 1.1 缩进
> 统一使用两个空格进行缩进,能让代码更加紧凑，增加横向代码展示空间。让代码在非编辑器环境下展示可读性更高

```typescript
// BAD: 
const badIndent = {
    a: 'string',
}

// GOOD: 
const goodIndent = {
  a: 'string',
}
```



### 1.2 换行
> 当单行无法容下参数声明时, 在多行显示, 且参数必须对齐. 同理, 类成员, 数组成员接口成员也需要对齐，增加可读性

```typescript
 // BAD: 
function foo( a: number, b: string, c: boolean, d: { a: number; b: string } )

interface Foo { a: number, b: string, }


// GOOD: 
 
function fooo(
  a: number,
  b: string,
  c: boolean,
  d: { a: number; b: string }
)

interface Fooo {
  a: number,
  b: string,
}
```


### 1.3 引号
> 使用单引号,统一单引号增强代码可读性; 单引号更容易输入;对于JSX, 字符串是使用双引号, 这是遵循XML的规范

```typescript
// BAD: 
const str = "string"

// GOOD: 
const str = 'string'

//BAD: 

function jsx() {
  return <div str='string' />
}
// GOOD: 
function jsx() {
  return <div str="string" />
}
```


### 1.4 行宽
> 最大行宽不超过80,增加可读性，能更好的显示代码和在非编辑器环境预览代码.


```typescript
// BAD
const veryverylongArray = ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'night']

//Good
const veryverylongArrayo = [
  'one',
  'two',
  'three',
  'four',
  'five',
  'six',
  'seven',
  'eight',
]
```

### 1.5 最大行数
> 为了更好地阅读和定位代码, 当你的文件超过500行时,就需要考虑将文件分割为多个文件了

### 1.6 逗号
> 对于跨越多行的数组字面量,对象字面量, import, export, type字面量 ,  函数形参列表 ,  函数调用实参等, 都应该尾随逗号,这可以让git diffs信息更加简洁. typescript会在编译阶段自动移除多余的逗号，所以不需要担心兼容性问题

```typescript
// BAD  
const notrailingWhitespace = { foo: 'string', bar: 1 }

const story = [ once , upon , aTime ]

import { Foo, Bar, Baz } from ‘./Foo’

function foo( bar: number, baz: string ) {/…/}

// GOOD
const trailingWhitespace = {
  foo: 'string',
  bar: 1,
}

const story = [
  once,
  upon,
  aTime,
]

import {
  Foo,
  Bar,
  Baz,
} from './Foo'

function foo(
  bar: number,
  baz: string,
) {/*...*/}
```

## 2. 命名规则
> 使用驼峰式命名`对象、函数和实例`

```typescript
// BAD
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}

//GOOD
const thisIsMyObject = {};
function thisIsMyFunction() {}
```
> 始终使用PascalCased形式命名`类, type alias, interface, namespace`等

```typescript
// BAD: 
declare class className {}

// GOOD: 
declare class ClassName {}
```

> 官方不建议为`接口`添加I前缀和类一样, 接口使用PascalCased格式,尽管对Java/C#程序员来说是很正常的事情. JavaScript标准库接口的惯例是没有I开始的,比如Window, Document.另外和Java或C#不同的是，Typescript中的类也可以被implement 或被接口extends, 即类和接口的界限不是十分突出

```typescript
// BAD
interface IInterfaceName {}

// GOOD
interface InterfaceName {}
```
> 不要使用下划线_开头或者结尾来命名属性。在某些情况，Javascript程序员习惯使用_ 开头来命名私有属性， 但是Typescript中有完善的访问描述符，所以应该避免使用下划线
```typescript
// BAD
class Foo {
  _bar: number
  // ... other
}
// GOOD
class Foo {
  private bar: number
  // ... other
}
```

> 避免单字母命名。命名应该具备描述性
```typescript
// BAD
function q() {
  // ...stuff...
}

// GOOD
function query() {
  // ..stuff..
}
```


> 如果文件中只输出一个类，文件命名和默认导出保持一致
```typescript
/**
 * Select文件
 */
// ...
export default class Select extends React.Component {
  // ...
}

// BAD
import CheckBox from './checkBox'
// or
import CheckBox from './check_box'

// GOOD: . 换句话说就是
import CheckBox from './CheckBox'
```

> 使用UPPER_SNAKE_CASE来命名常量

```ts
// BAD
const platform = 'android'

// GOOD
const PLATFORM = 'android'
```

## 注释
> 使用"//" 作为单行注释, 注释内容前面必须有空格
```ts
// BAD: 
//bad

// GOOD
// good
```
> 每个文件开头必须提供关于这个文件的注释.说明文件的内容, TODO, 更新日期, 权限等信息
```ts
// BAD
export default function Title() {}
// GOOD:  
/**
  Title bala bala bala
  @example
*/

export default function Title() {}
```
> 使用/** ...*/作为多行注释, 并使用JSDoc格式对代码进行文档化
```typescript
// `BAD`

// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
function make(tag) {

  // ...stuff...

  return element
}

// GOOD:  
 /**
  make() returns a new element
  based on the passed in tag name *
  @param {String} tag
  @return {Element} element 
*/ 
function make(tag) {
  // …stuff…

  return element 
}
```

> `FIXME`注释标注问题可以帮助其他开发者快速了解这是一个需要复查的问题，`TODO`注释标注问题的解决方式 ,给需要实现的功能提供一个解决方式。可以使用`Atom`编辑器的`todo-show`插件，或者`VSCode`的`TODO Parser`插件来解析、查找和处理的你项目中的TODO和FIXME注释
```typescript
class Calculator {
  constructor() {
    // FIXME: shouldn't use a global here
    total = 0;
  }
}

class Calculator {
  constructor() {
    // TODO: total should be configurable by an options param
    this.total = 0;
  }
}
```

### 4. 函数
### 4.1 箭头函数
> 只有一个参数时,可以省略括号
```ts
// BAD: 
const arrowFunction = (i) => i 

// GOOD: 
const arrowFunctiono = i => i 
```
> 如果可以尽量使用简写的返回
```ts
// BAD: 
const shorthandReturn = () => { return true }

// GOOD: 
const shorthandReturno = () => true
```
>别保存 this 的引用。优先使用箭头函数
```typescript
// BAD  
function foo() { const self = this return function() { console.log(self) } }
function foo() { const that = this return function() { console.log(that) } }

// `GOOD`: 
function foo() {
  return () => {
    console.log(this)
  }
}
```
### 4.2　函数
> new 操作始终加上()
```ts
// BAD: 
let date = new Date
// GOOD: 
date = new Date()
```
> 使用函数声明代替函数表达式,因为函数声明是可命名的，所以他们在调用栈中更容易被识别。此外，函数声明会把整个函数提升（hoisted），而函数表达式只会把函数的引用变量名提升
```ts
// BAD
const foo = function () {
}

// GOOD: 
function foo() {
}
```
> 不要使用 arguments。可以选择 rest 语法 ... 替代,使用 … 能明确你要传入的参数, 可以被类型检查。另外 rest 参数是一个真正的数组，而 arguments 是一个类数组
```typescript
// BAD  
function concatenateAll() { const args = Array.prototype.slice.call(arguments); return args.join(''); }
function proxy() { foo.apply(null, arguments) }

// `GOOD`: 。
function concatenateAll(...args) {
  return args.join('');
}

function proxy(...args) {
  foo(...args)
}
```

## 5. 对象
> 只有在必要时, 才添加引号
```ts
// BAD: 
const obj = {
  'foo': 'string',
  'foo bar': 1,
}

// GOOD: 
const objo = {
  foo: 'string',
  'foo bar': 1,
}
```
> 优先使用对象简写模式
```ts
// BAD: 
const shorthandObj = {
  obj: obj,
  foo: 'string',
}

// GOOD: 

const shorthandObjo = {
  obj,
  foo: 'string',
}
```
> 优先使用object spread 语法
```ts
// BAD: 
const obj1 = {
  a: 1,
  b: 2,
}
let objectAssign = Object.assign({}, obj1)

// GOOD: 
let objectSpread = { ...obj1 }
```

## 6. 操作符/表达式
> 二元操作符中的字面量应该始终在变量的右边
```ts
// BAD: 
const x = 1
const binaryOperation = 1 + x
// GOOD:
const binaryOperationo = x + 1
```
> 不要比较boolean 字面量
```ts
// BAD: 
const ok: boolean = true
let baz = ok === true ? 'foo' : 'baz'

// GOOD: 
baz = ok ? 'foo' : 'baz'
```
> 当使用if语句比较超过三个时, 考虑使用switch
```ts
// BAD: 
const type: string = 'foo'
if (type === 'foo') {
  console.log('foo')
} else if (type === 'bar') {
  console.log('bar')
} else if (type === 'baz') {
  console.log('baz')
} else {
  console.log('default')
}

// GOOD: 
switch (type) {
  case 'foo':
    console.log('foo')
    break
  case 'bar':
    console.log('bar')
    break
  case 'baz':
    console.log('baz')
    break
  default:
    console.log('default')
}
```
> 优先使用字符串模板

```ts
// BAD:
const hello = 'hello'
const world = 'world'
let temp = 'print' + hello + ' ' + world

// GOOD: 
temp = `print${hello} ${world}`
```

## 7. 模块
> 导入默认导出, 最好匹配库默认的导出名
```ts
// BAD
import IReact from 'react'
// GOOD: 
import React from 'react'
```
> 为了减少打包体积, 避免引入整个模块, 而是按需引入需要的子模块. 典型的应用就是lodash
```ts
// BAD
import _ from 'lodash'
// GOOD: 
import findIndex from 'lodash/findIndex'
```
> 为了区分静态资源和JavaScript模块, 我们使用require 来加载静态资源, 使用import来导入Javascript模块
```ts
// BAD
import myIcon from 'assets/icons/github.svg'

// GOOD:  
import Foo from './path/to/foo'
```
```html
<Icon src={require('assets/icons/myicon.svg')} /> 
<img src={require('assets/images/bg.png')} />
```
> 优先使用非相对路径来导入模块, 从而避免`路径地狱`. 使用相对路径还不利于模块的移动. 通过设置tsconfig.json的paths选项和webpack的resolve.modules或resolve.alias 来实现模块查找, 比如将src的根目录设置为node模块的查找目录
```ts
//  `BAD`
// container/Foo/bar.ts
import Baz from '../../components/Baz'
// GOOD: 
import Baz from 'components/Baz'
```
> 避免使用webpack提供的非标准的模块加载语法, 尽量使用ES6模块
```ts
// BAD
require.ensure(['mymodule'], require => {
  const myModule = require('mymodule')
  // ...
})
// GOOD: 
import('mymodule').then(module => {/*...*/})
```

## 8. 接口
> 优先使用接口来代替type, 因为接口可以被实现, 扩展和合并
```ts
// BAD:
type t = {
  foo: number,
  bar: string,
}
GOOD: 

interface To {
  foo: number,
  bar: string,
}
```

## 9. 类
> 始终显式设置成员的可见性, 这样可以提醒你慎重考虑属性的可见性, 避免将因为省略描述符而将私有成员暴露出去
```ts
// BAD:
class Member {
  foo() {
    // do somthing
  }
}
// GOOD: 
class Membero {
  public foo() {
    // do somthing
  }
}
```
> 使用`class properties`初始化类变量和实例变量, 配合`箭头函数`可以绑定方法的`this`上下文
```ts
// BAD 
class Foo extends React.Component { constructor() { this.bar = this.bar.bind(this) } 
bar () { console.log('baz') } 
render() { return <button onClick={this.bar}> } }
class Foo extends React.Component { bar () { console.log('baz') } 
render() { return <button onClick={this.bar.bind(this)}> } }
//  `GOOD`: 
class Foo extends React.Component {
  // 静态属性
  static defaultProps = {
    prop1: 1
  }
  // 实例属性
  baz: number = 0
  // 配合箭头函数绑定上下文
  bar = () => {
    console.log('baz')
  }
  render() {
    return <button onClick={this.bar}>
  }
}
```