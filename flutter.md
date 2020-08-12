# flutter dart 代码规范
## 空格
## 换行
> 官方推荐，每行代码不超过80个字符。太长的单行显示不利于阅读

## 括号
> 推荐流程控制相关语句都要加花括号{…}，防止出现其他错误，也更有利于排版和阅读。

```dart
if (isWeekDay) {
    print('Bike to work!');
} else {
    print('Go dancing or read a book!');
}
```

> 但是如果一个控制语句只有if，没有else的话，可以不使用{}：
```dart
if (arg == null) return defaultValue;
```

> 但是，如果if里的判断语句和return的返回的语句内容都很长，可能会产生换行，这种推荐要加花括号{…}：
```dart
if (overflowChars != other.overflowChars) {
  return overflowChars < other.overflowChars;
}
```

## 编辑器设置
> 使用dartfmt插件进行格式化代码


## 命名
> 大驼峰命名类名、枚举、typedef、方法参数类型
```dart
    //类名命名
    class ItemMenu { ... }

    class HttpApi { ... }

    //注解
    @Foo()
    class A { ... }

    //枚举
    enum Color {
    LightRed, 
    LightBlue
    }

    //typedef
    typedef Predicate<T> = bool Function(T value);

    //方法参数类型
    @override
    Widget build(BuildContext context) {...}
```

> 小驼峰命名变量名、方法和参数名称命名、常量

```dart
    //变量命名
    var item;

    HttpRequest httpRequest;

    //方法和参数名称命名
    void align(bool clearItems) {
    // ...
    }
    //常量名称定义
    const pi = 3.14;
    const defaultTimeout = 1000;
    final urlScheme = RegExp('^([a-z]+):');

    class Dice {
    static final numberGenerator = Random();
    }
```

> 蛇形命名文件名、文件夹名、导入类库时候的as关键字后面的命名

目录文件夹命名可以类似：http_utils这种形式
源代码文件命名可以类似：screen_utils.dart这种形式

```dart
import 'dart:math' as math;
import 'package:angular_components/angular_components'
    as angular_components;
import 'package:js/js.dart' as js;
```
> 不要使用前缀字母，如mHttp，kHttp这种形式。
```dart
//推荐
defaultTimeout
//不推荐使用
kDefaultTimeout
```

> dart包的导入要写在package包的前面
```dart
import 'dart:async';
import 'dart:html';

import 'package:bar/bar.dart';
import 'package:foo/foo.dart';
```
> package:包的导入要写在我们相对引用本项目类的前面
```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'util.dart';
```
> 将自己的包内的类的引入放置在其他第三方库引入的包后面
```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'package:my_package/util.dart';
```
> export的引入要写在import引入的后面
```dart
import 'src/error.dart';
import 'src/foo_bar.dart';

export 'src/error.dart';
```

> 同级别的引用排列顺序最好按照字母的顺序进行排列
```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'foo.dart';
import 'foo/foo.dart';
```
> 某个方法和常量、变量、类不想被外部其他类调用时用的话，在相应的名称前加_下划线前缀即可，
```dart
//这样这个类就不能被其他类访问调用到了
class _MyMainPageState extends State<MyMainApp> {
  @override
  void initState() {
    super.initState();
  }
```
## 文件
> `assets` 目录放置静态资源文件

    assets
    └─ audios
    ├─ vedios
    └─ images
    └─ fonts

* 如果没有其他太多的资源，把资源文件都放在assets目录下即可。这个assets目录默认是没有的，我们可以在项目根目录新建一个assets目录用于存放应用使用的资源文件。

> `lib` 目录组织，默认创建在lib目录下只有一个main.dart文件，这是整个应用的入口文件，这个main.dart名称不可以修改、。lib里的其他类可以按照供能进行划分目录，自己建立相应的分类目录即可。

    lib
    └─ api
    ├─ config
    └─ ui
    └─ utils
    └─ widgets
    └─ main.dart

## 异步任务编程
> 使用Future和async、await来进行处理异步编程，async和await最后成对出现
```dart
//推荐写法
Future<int> countActivePlayers(String teamName) async {
  try {
    var team = await downloadTeam(teamName);
    if (team == null) return 0;

    var players = await team.roster;
    return players.where((player) => player.isActive).length;
  } catch (e) {
    log.error(e);
    return 0;
  }
}
//不推荐写法
Future<int> countActivePlayers(String teamName) {
  return downloadTeam(teamName).then((team) {
    if (team == null) return Future.value(0);

    return team.roster.then((players) {
      return players.where((player) => player.isActive).length;
    });
  }).catchError((e) {
    log.error(e);
    return 0;
  });
}
```

> 如果有些方法功能没有用到异步任务，不要加async关键字
```dart
//推荐写法
Future afterTwoThings(Future first, Future second) {
  return Future.wait([first, second]);
}
//不推荐写法
Future afterTwoThings(Future first, Future second) async {
  return Future.wait([first, second]);
}
```

> 关于数据转换我们可以用Future里高级用法来简化操作
```dart
//推荐写法
Future<bool> fileContainsBear(String path) {
  return File(path).readAsString().then((contents) {
    return contents.contains('bear');
  });
}
//推荐写法
Future<bool> fileContainsBear(String path) async {
  var contents = await File(path).readAsString();
  return contents.contains('bear');
}
//不推荐写法
Future<bool> fileContainsBear(String path) {
  var completer = Completer<bool>();

  File(path).readAsString().then((contents) {
    completer.complete(contents.contains('bear'));
  });

  return completer.future;
}
```

> 可以适当的使用T泛型
```dart
//推荐写法
Future<T> logValue<T>(FutureOr<T> value) async {
  if (value is Future<T>) {
    var result = await value;
    print(result);
    return result;
  } else {
    print(value);
    return value as T;
  }
}
//不推荐写法
Future<T> logValue<T>(FutureOr<T> value) async {
  if (value is T) {
    print(value);
    return value;
  } else {
    var result = await value;
    print(result);
    return result;
  }
}
```

## 异常处理
> 可以使用rethrow重新处理后抛出异常，以提供给其他后续逻辑处理
```dart
//推荐
try {
  somethingRisky();
} catch (e) {
  if (!canHandle(e)) rethrow;
  handle(e);
}
//不推荐
try {
  somethingRisky();
} catch (e) {
  if (!canHandle(e)) throw e;
  handle(e);
}
```

## 函数方法
> 函数的方法里面函数定义使用声明式定义
```dart
//推荐写法
void main() {
  localFunction() {
    ...
  }
}
//不推荐写法
void main() {
  var localFunction = () {
    ...
  };
}
```
> 能简写的尽量简写
```dart
//推荐写法
names.forEach(print);
//不推荐写法
names.forEach((name) {
  print(name);
});
```

> 用等号将默认值和参数分隔
```dart
//推荐写法
void insert(Object item, {int at = 0}) { ... }
//不推荐写法
void insert(Object item, {int at: 0}) { ... }
```

> 可以使用??两个问号来判断是否是null
```dart
void error([String message]) {
  stderr.write(message ?? '\n');
}
```
> 不要将变量初始化为null
```dart
//推荐写法
int _nextId;

class LazyId {
  int _id;

  int get id {
    if (_nextId == null) _nextId = 0;
    if (_id == null) _id = _nextId++;

    return _id;
  }
}
//不推荐写法
int _nextId = null;

class LazyId {
  int _id = null;

  int get id {
    if (_nextId == null) _nextId = 0;
    if (_id == null) _id = _nextId++;

    return _id;
  }
}
```
> 不用写类成员变量的getter和setter方法，默认是隐藏自带的
```dart
//推荐写法
class Box {
  var contents;
}

//不推荐
class Box {
  var _contents;
  get contents => _contents;
  set contents(value) {
    _contents = value;
  }
}
```
> 可以使用final来创建只读常量，也支持=>简写
```dart
class Box {
  final contents = [];
}
//=>也就是省略了{...}和return
double get area => (right - left) * (bottom - top);
```

> 不推荐重复多次使用this关键字
```dart
//推荐写法
class Box {
  var value;

  void clear() {
    update(null);
  }

  void update(value) {
    this.value = value;
  }
}
//不推荐写法
class Box {
  var value;

  void clear() {
    this.update(null);
  }

  void update(value) {
    this.value = value;
  }
}
```
> 尽量在声明中初始化常量
```dart
//推荐
class Folder {
  final String name;
  final List<Document> contents = [];

  Folder(this.name);
  Folder.temp() : name = 'temporary';
}
//不推荐
class Folder {
  final String name;
  final List<Document> contents;

  Folder(this.name) : contents = [];
  Folder.temp() : name = 'temporary'; // Oops! Forgot contents.
}

```
> 缩减构造方法初始化写法
```dart
//推荐
class Point {
  num x, y;
  Point(this.x, this.y);
}
//不推荐
class Point {
  num x, y;
  Point(num x, num y) {
    this.x = x;
    this.y = y;
  }
}
```
> 构造方法里无需重复声明参数类型
```dart
//推荐
class Point {
  int x, y;
  Point(this.x, this.y);
}
//不推荐
class Point {
  int x, y;
  Point(int this.x, int this.y);
}
```
> 对于空方法体的构造方法直接写不用结尾{}
```dart
//推荐
class Point {
  int x, y;
  Point(this.x, this.y);
}
//不推荐
class Point {
  int x, y;
  Point(this.x, this.y) {}
}
```

> new关键字可以不写，dar2已经支持不写new关键字了
```dart
//推荐
Widget build(BuildContext context) {
  return Row(
    children: [
      RaisedButton(
        child: Text('Increment'),
      ),
      Text('Click!'),
    ],
  );
}
//不推荐
Widget build(BuildContext context) {
  return new Row(
    children: [
      new RaisedButton(
        child: new Text('Increment'),
      ),
      new Text('Click!'),
    ],
  );
}
```
> 无需重复定义const关键字
```dart
//推荐
const primaryColors = [
  Color("red", [255, 0, 0]),
  Color("green", [0, 255, 0]),
  Color("blue", [0, 0, 255]),
];
//不推荐
const primaryColors = const [
  const Color("red", const [255, 0, 0]),
  const Color("green", const [0, 255, 0]),
  const Color("blue", const [0, 0, 255]),
];
```
## 集合lists, maps, queues, sets
> 字面量创建集合
```dart
//推荐
var points = [];
var addresses = {};
var points = <Point>[];
var addresses = <String, Address>{};
var iterable = [1, 2, 3];

//不推荐的
var points = List();
var addresses = Map();
var points = List<Point>();
var addresses = Map<String, Address>();
```

> 使用isEmpty和isNotEmpty来判断集合是否为空
```dart
// 推荐
if (lunchBox.isEmpty) return 'so hungry...';
if (words.isNotEmpty) return words.join(' ');

// 不推荐
if (lunchBox.length == 0) return 'so hungry...';
if (!words.isEmpty) return words.join(' ');
```

> 对于集合转换，使用它的链式高级方法来转换
```dart
var aquaticNames = animals
    .where((animal) => animal.isAquatic)
    .map((animal) => animal.name);
```

> 集合的循环遍历推荐使用for
```dart
// 推荐
for (var person in people) {
  ...
}

// 不推荐
people.forEach((person) {
  ...
});
```

> List.toList来进行类型转换
```dart
// 推荐
var copy1 = iterable.toList();
//不推荐
var copy2 = List.from(iterable);
```

> 但是如果改变集合类型，这是可以使用List.from方法
```dart
var numbers = [1, 2.3, 4]; // List<num>.
numbers.removeAt(1); // Now it only contains integers.
var ints = List<int>.from(numbers);

var stuff = <dynamic>[1, 2];
var ints = List<int>.from(stuff);
```

> 使用objects.whereType 进行集合过滤
```dart
//不推荐
var objects = [1, "a", 2, "b", 3];
var ints = objects.where((e) => e is int);

var objects = [1, "a", 2, "b", 3];
var ints = objects.where((e) => e is int).cast<int>();

//推荐
var objects = [1, "a", 2, "b", 3];
var ints = objects.whereType<int>();
```

## 字符串
> 字符串连接不需要用+号连接，直接挨着写即可：
```dart 
// 推荐
raiseAlarm(
    'ERROR: Parts of the spaceship are on fire. Other '
    'parts are overrun by martians. Unclear which are which.');
    ...
'Hello, $name! You are ${year - birth} years old.';

//不推荐
raiseAlarm('ERROR: Parts of the spaceship are on fire. Other ' +
    'parts are overrun by martians. Unclear which are which.');
    ...
'Hello, ' + name + '! You are ' + (year - birth).toString() + ' y...';
```

 
## 包导入
假如我们包结构如下：

    my_package
    └─ lib
    ├─ src
    │  └─ utils.dart
    └─ api.dart

> 在api.dart中想引入src下的utils.dart类，推荐相对路径引入：

```dart
//推荐
import 'src/utils.dart';

//不推荐
import 'package:my_package/src/utils.dart';
```
## 注释
> Flutter也支持在文档注释里加入MarkDown文本,但是我们应该避免过度使用MarkDown，这样可能会导致文档注释非常混乱，不利于阅读使用。
```dart
/// 这个是正常的文字
///
///
/// * MarkDown符号
/// * MarkDown符号
/// * MarkDown符号
///
/// 1. MarkDown列表
/// 2. MarkDown列表
/// 1. MarkDown列表
///
///     * MarkDown列表
///     * MarkDown列表
///     * MarkDown列表
///
/// MarkDown语法都支持:
///
/// ```
/// this.code
///     .will
///     .retain(its, formatting);
/// ```
///
/// The code language (for syntax highlighting) defaults to Dart. You can
/// specify it by putting the name of the language after the opening backticks:
///
/// ```html
/// <h1>HTML is magical!</h1>
/// ```
///
/// Links can be:
///
/// * http://www.just-a-bare-url.com
/// * [with the URL inline](http://google.com)
/// * [or separated out][ref link]
///
/// [ref link]: http://google.com
///
/// # A Header
///
/// ## A subheader
///
/// ### A subsubheader
///
/// #### If you need this many levels of headers, you're doing it wrong
```
> 不推荐使用缩进空格的注释：
---推荐注释
```dart
/// You can use [CodeBlockExample] like this:
///
/// ```
/// var example = CodeBlockExample();
/// print(example.isItGreat); // "Yes."
/// ```
```
---不推荐
```dart
/// You can use [CodeBlockExample] like this:
///
///     var example = CodeBlockExample();
///     print(example.isItGreat); // "Yes."
```

>使用文档注释///来注释类成员和类型、方法、参数、类、变量常量等
```dart
/// 这个是获取字符长度
int get length => ...
```

> 多行注释/**/用来注释代码,不推荐用多行注释来写单行注释

```dart
/*
class _MyMainPageState extends State<MyMainApp> {
  @override
  void initState() {
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      //页面
      home: Scaffold(
        appBar: AppBar(
          title: Text('标题'),
        ),
        body: getBody(),
      ),
    );
  }

  Widget getBody() {
    return Center(child: Text("我是内容"));
  }
}
*/

```

> 如果遇到一些层级嵌套太深的情况下，你也可以将某个层级定义为另一个方法进行调用引入即可。
```dart
class _MyMainPageState extends State<MyMainApp> {
  @override
  void initState() {
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('标题'),
        ),
        //通过方法引入
        body: getBody(),
      ),
    );
  }

  Widget getBody() {
    return Center(child: Text("我是内容"));
  }
}

```
