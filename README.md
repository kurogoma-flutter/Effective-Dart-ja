# Effective-Dart-ja
EffectiveDartを簡易的に日本語訳しました（執筆中）

# 命名規約
### 識別子
#### クラス、Enum、型、typedefs、型指定の引数ではアッパーキャメルケースにすべき
#### extensionする場合もアッパーキャメルケースにすべき
#### ライブラリ、パッケージ、ディレクトリ、ファイル名はスネークケースにすべき
#### インポートのプレフィックスを用いる場合もスネークケースにすべき
```dart
// GOOD
import 'package:angular_components/angular_components.dart' as angular_components;
```
#### 変数名はローワーキャメルケースにすべき
#### 定数名はローワーキャメルケースが好ましい
```dart
//BAD
final URL_SCHEME = RegExp('^([a-z]+):');
```
#### 2文字の略語は全て大文字で表記すべき
```dart
// GOOD
class TVPlayer {}

// BAD
class TvPlayer {}
```
#### コールバックやパラメーターを用いない場合は、`_`を用いるのが好ましい
#### プライベートではない変数やメソッドに`_`は用いてはいけない
#### 接頭辞（意味を持たない単語）は用いてはいけない
```dart
// BAD
kDefaultTimeout
```

### 序列
#### `dart:`で始まるインポートは`package:`より上に記述すべき
#### `package:`で始まるインポートはプロジェクトファイルのインポートより上に記述すべき
#### exportは、importから下に１行開けて記述すべき
```Dart
// GOOD
import 'src/error.dart';
import 'src/foo_bar.dart';

export 'src/error.dart';
```
#### それぞれアルファベット順に並べるべき

### フォーマット・整形
#### フォーマット・整形フォーマットには[dart format](https://dart.dev/tools/dart-format)を用いるべき
#### フォーマットしやすいようコードを書くよう心がけてください。
#### １行80文字以上になるのは避けたほうが良い
#### 処理部分には中括弧`{}`を用いるようにしてください。（1行のif文は良い）
```dart
// GOOD
if (isWeekDay) {
  print('Bike to work!');
} else {
  print('Go dancing or read a book!');
}

if (arg == null) return defaultValue;

// BAD
if (overflowChars != other.overflowChars)
  return overflowChars < other.overflowChars;
```

# コメント
#### コメントは文章のように記述すべき
#### ブロックコメントは使うべきではない
#### メンバーや型にコメントを付ける場合は、`///`を用いるべき
#### パブリックAPIに対するコメントは記述すべき
#### ライブラリのようなレベルのコメントを書くよう心がけてください
#### プライベートAPIにもコメントを書くよう心がけてください
#### コメントは１行で簡潔に記述すべき
#### 説明のコメントと、パラメータに対するコメントは分離すべき
```Dart
// GOOD
/// Deletes the file at [path].
///
/// Throws an [IOError] if the file could not be found. Throws a
/// [PermissionError] if the file is present but could not be deleted.
void delete(String path) {
  ...
}
```
#### 一目してわかるメソッドや変数に対するコメントは避けるべき。命名に組み込むようにすべき
#### メソッドについてのコメントは動詞で始めるようにしてください
```dart
// GOOD
/// Starts the stopwatch if not already running.
void start() {
  ...
}
```
#### 変数、ゲッター、セッターについてのコメントは名詞でスタートするようにしてください
```dart
// GOOD
/// The number of checked buttons on the page.
int get checkedCount => ...
```

#### ライブラリ、クラスや型についてのコメントは名詞でスタートするようにしてください
#### コメントにサンプルを入れるよう心がけましょう
```dart
/// Returns the lesser of two numbers.
///
/// ```dart
/// min(5, 3) == 3
/// ```
num min(num a, num b) => ...
```
#### 変数、型、引数、メソッドなどのコメントは角カッコ'[]'を用いるべき
```dert
// GOOD
/// Throws a [StateError] if ...
/// similar to [anotherMethod()], but ...
/// To create a point, call [Point.new] or use [Point.polar] to ...
```
#### メソッドやクラスのパラメーターの説明は散文（区切りのない文章）で記述すべき
```dart
// BAD
/// Defines a flag with the given name and abbreviation.
///
/// @param name The name of the flag.
/// @param abbr The abbreviation for the flag.
/// @returns The new flag.
/// @throws ArgumentError If there is already an option with
///     the given name or abbreviation.
Flag addFlag(String name, String abbr) => ...

// GOOD
/// Defines a flag.
///
/// Throws an [ArgumentError] if there is already an option named [name] or
/// there is already an option using abbreviation [abbr]. Returns the new flag.
Flag addFlag(String name, String abbr) => ...
```

#### コメントはアノテーションの上に記述すべき
```dart
// BAD
@Component(selector: 'toggle')
/// A button that can be flipped on and off.
class ToggleComponent {}

// GOOD
/// A button that can be flipped on and off.
@Component(selector: 'toggle')
class ToggleComponent {}
```

### コメントにはマークダウンが利用できます。
```dart
/// This is a paragraph of regular text.
///
/// This sentence has *two* _emphasized_ words (italics) and **two**
/// __strong__ ones (bold).
///
/// A blank line creates a separate paragraph. It has some `inline code`
/// delimited using backticks.
///
/// * Unordered lists.
/// * Look like ASCII bullet lists.
/// * You can also use `-` or `+`.
///
/// 1. Numbered lists.
/// 2. Are, well, numbered.
/// 1. But the values don't matter.
///
///     * You can nest lists too.
///     * They must be indented at least 4 spaces.
///     * (Well, 5 including the space after `///`.)
///
/// Code blocks are fenced in triple backticks:
///
/// ```dart
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
/// * https://www.just-a-bare-url.com
/// * [with the URL inline](https://google.com)
/// * [or separated out][ref link]
///
/// [ref link]: https://google.com
///
/// # A Header
///
/// ## A subheader
///
/// ### A subsubheader
///
/// #### If you need this many levels of headers, you're doing it wrong
```

#### 過剰にマークダウンを用いるのは避けるべき
#### HTMLタグは避けるべき
#### コードブロックにはバックティック&#096;を用いるべき
#### 簡潔にすべき
#### 明らかに伝わる場合を除き、略語や頭字語は避けるべき
#### The ~よりthisを用いたほうが良い


# 使用例
### ライブラリ
#### ライブラリやパッケージ、part ofは文字列で記述すべき
```dart
// GOOD
part of '../../my_library.dart';
// BAD
part of my_library;
```
#### 他のプロジェクトのsrc配下にあるライブラリはインポートしてはいけない
#### libの外からlibディレクトリ配下のファイルをインポートする場合、libをパスに入れてはいけない。`package:`を用いるべき
```dart
// BAD
import '../lib/api.dart';

// GOOD
import 'package:my_package/api.dart';
```

### Null
#### 初期値でnullを設定することはしてはならない
```Dart
// BAD
Item? bestItem = null;
```
#### メソッドの引数の初期値にnullを設定してはならない
```dart
// BAD
void error([String? message = null]) {
  stderr.write(message ?? '\n');
}
```
#### nullかどうかでtrue, falseを決めたい場合、`==`ではなく`??`を用いるべき
```dart
// BAD
// If you want null to be false:
if (optionalThing?.isEnabled ?? false) {
  print('Have enabled thing.');
}

// GOOD
// If you want null to be false:
if (optionalThing?.isEnabled == true) {
  print('Have enabled thing.');
}
```
#### 初期化されているか定かではない場合、lateで変数定義をするのは避けるべき
#### 余計なnullチェックはしない
```dart
// BAD
class UploadException {
  final Response? response;

  UploadException([this.response]);

  @override
  String toString() {
    // ここでnullチェックをするので後続の「！」は不要になる
    if (response != null) {
      return 'Could not complete upload to ${response!.url} '
          '(error code ${response!.errorCode}): ${response!.reason}.';
    }

    return 'Could not upload (no response).';
  }
}
```

### String
#### 文字列に改行がある場合、`+`ではなく隣接させて用いる
```dart
// BAD
raiseAlarm('ERROR: Parts of the spaceship are on fire. Other ' +
    'parts are overrun by martians. Unclear which are which.');

// GOOD
raiseAlarm('ERROR: Parts of the spaceship are on fire. Other '
    'parts are overrun by martians. Unclear which are which.');
```

#### 文字連結より、補間を用いる
```dart
// BAD
'Hello, ' + name + '! You are ' + (year - birth).toString() + ' y...';
// GOOD
'Hello, $name! You are ${year - birth} years old.';
```

#### 不要な中括弧は避けるべき
```dart
// BAD
var greeting = 'Hi, ${name}! I love your ${decade}s costume.';

// GOOD
var greeting = 'Hi, $name! I love your ${decade}s costume.';
```

### Collections
#### Map, List, Setの定義は可能な限り以下のように記述すべき
```dart
// BAD
var addresses = Map<String, Address>();
var counts = Set<int>();
// GOOD
var addresses = <String, Address>{};
var counts = <int>{};
```

#### collectionのデータの有無を確かめるために`.length()`を用いてはならない
```dart
// BAD
if (lunchBox.length == 0) return 'so hungry...';

// GOOD
if (lunchBox.isEmpty) return 'so hungry...';
```

#### 関数内の処理で、`forEach`は避けるべき
```dart
// BAD
people.forEach((person) {
  ...
});

// GOOD
for (final person in people) {
  ...
}
```
#### `List.from()は使わず、`toList()`を用いるべき
#### コレクションをデータ型で絞り込みたい場合、`whereType()`を用いるべき
```dart
// BAD
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.where((e) => e is int).cast<int>();

// GOOD
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.whereType<int>();

// (1, 2, 3)
```
#### 同じ型だと推定できるのに`cast()`を用いてはならない
```dart
var stuff = <dynamic>[1, 2];
// BAD
var ints = stuff.toList().cast<int>();

// GOOD
var ints = List<int>.from(stuff);
```
#### そもそも`cast()`は使用を避ける

### Functions
#### 関数は内部で関数を定義したい場合、以下のように記述すべき
```dart
// BAD
void main() {
  var localFunction = () {
    ...
  };
}

// GOOD
void main() {
  void localFunction() {
    ...
  }
}
```

#### `forEach`や`map`は省略できる部分はすべき
```Dart
// BAD
// Method:
charCodes.forEach((code) {
  buffer.write(code);
});

// Named constructor:
var strings = charCodes.map((code) => String.fromCharCode(code));

// GOOD
// Method:
charCodes.forEach(buffer.write);

// Named constructor:
var strings = charCodes.map(String.fromCharCode);
```
#### 名前付き引数の初期値は`=`を用いて設定すべき
```dart
// BAD
void insert(Object item, {int at: 0}) { ... }

// GOOD
void insert(Object item, {int at = 0}) { ... }
```

### Variables

#### 変数定義で用いるvarとfinalは適切に使い分けてください
#### 計算できるものについて、一々分割して保存をしない。
```dart
// BAD
class Circle {
  double _radius;
  double get radius => _radius;
  set radius(double value) {
    _radius = value;
    _recalculate();
  }

  double _area = 0.0;
  double get area => _area;

  double _circumference = 0.0;
  double get circumference => _circumference;

  Circle(this._radius) {
    _recalculate();
  }

  void _recalculate() {
    _area = pi * _radius * _radius;
    _circumference = pi * 2.0 * _radius;
  }
}

// GOOD
class Circle {
  double radius;

  Circle(this.radius);

  double get area => pi * radius * radius;
  double get circumference => pi * 2.0 * radius;
}
```


### Members
#### getterやsetterが不要な場合、排除すべき
#### 変更されない値（読み取り専用）の場合、finalを用いたほうがよい
#### アロー関数で簡潔にできる場合は、そうすべき
#### クラス内に同名のプロパティがある場合や、名前付きコンストラクタにリダイレクトする場合を除き、`this.`の表現はDartでは不要です
#### 可能な限り、変数定義の段階で値を入れておくこと

### Constructors
#### 可能な限り初期化は簡潔にすること
```dart
// BAD
class Point {
  double x, y;
  Point(double x, double y)
      : x = x,
        y = y;
}

// GOOD
class Point {
  double x, y;
  Point(this.x, this.y);
}
```

#### コンストラクタの初期化対象の変数に`late`を用いないでください。
```dart
// BAD
class Point {
  late double x, y;
  Point.polar(double theta, double radius) {
    x = cos(theta) * radius;
    y = sin(theta) * radius;
  }
}

// GOOD
class Point {
  double x, y;
  Point.polar(double theta, double radius)
      : x = cos(theta) * radius,
        y = sin(theta) * radius;
}
```
#### コンストラクタのbodyが空の場合、`{}`ではなく`;`を用いるべき
```dart
// BAD
class Point {
  double x, y;
  Point(this.x, this.y) {}
}

// GOOD
class Point {
  double x, y;
  Point(this.x, this.y);
}
```

#### コンストラクタの生成に`new`は使わない
#### `const`を（無駄に）重複して使わない
```dart
// BAD
const primaryColors = const [
  const Color('red', const [255, 0, 0]),
  const Color('green', const [0, 255, 0]),
  const Color('blue', const [0, 0, 255]),
];

// GOOD
const primaryColors = [
  Color('red', [255, 0, 0]),
  Color('green', [0, 255, 0]),
  Color('blue', [0, 0, 255]),
];
```

### Error handling
#### `try{}catch{}`の`catch`に`on`を含めないことは避けるべき
#### onの無いcatchでエラーを補足した場合、破棄してはならない（異常をユーザーに伝えるべき）
#### 例外で返すエラーは、プログラムエラーに留めるようにしてください。コードバグは伝えないようにすべき。
#### エラーの型に対し、明示的に受け取ってはならない。例外で処理が止まらず原因の特定に時間を要する。
#### 例外を再度throwする場合は、`rethrow`を用いるべき

### Asynchrony（非同期）
#### 生のFutureメソッドで実装するのではなく、async/awaitを用いるべき
```dart
// BAD
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

// GOOD
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
```

#### 無意味にasyncを用いてはならない
使っても良い例
- awaitが伴う場合
- Future.error()に該当する場合
- Future.value()に該当する場合

#### CONSIDER using higher-order methods to transform a stream.???

#### completerを直接用いるのは避けるべき

#### `DO test for Future<T> when disambiguating a FutureOr<T> whose type argument could be Object.??`

# 設計
### 命名
####  命名で用いる用語には一貫性を持たせること
```dart
// BAD
renumberPages()      // 誤解を生みやすい
convertToSomething() // to~ に親の単語は不要です
wrappedAsSomething() // as~ に親の単語は不要です
Cartesian            // 馴染みのない用語

// GOOD
pageCount         // A field.
updatePageCount() // Consistent with pageCount.
toSomething()     // Consistent with Iterable's toList().
asSomething()     // Consistent with List's asMap().
Point             // 一般的に知られている
```
 
#### 略語の使用は避ける
#### 最も説明的（主要）な単語は一番後ろにつける
```dart
// BAD
numPages                  // Not a collection of pages.
RuleFontFaceCss           // Not a CSS.

// GOOD
pageCount             // A count (of pages).
CssFontFaceRule       // A rule for font faces in CSS.
```
#### 文章を読むかのようなコード構成にすべき
```dart
// BAD
// Telling errors to empty itself, or asking if it is?
if (errors.empty) ...

// Toggle what? To what?
subscription.toggle();

// Filter the monsters with claws *out* or include *only* those?
monsters.filter((monster) => monster.hasClaws);

// GOOD
// "If errors is empty..."
if (errors.isEmpty) ...

// "Hey, subscription, cancel!"
subscription.cancel();

// "Get the monsters where the monster has claws."
monsters.where((monster) => monster.hasClaws);
```

#### bool値以外の変数には名詞を優先してつけるべき
```dart
// BAD
list.deleteItems

// GOOD
list.length
context.lineWidth
quest.rampagingSwampBeast
```
#### bool値の変数に対して、形容詞や名刺を優先してつけ、動詞は避けるべき
```dart
// BAD
empty         // 形容詞？名詞？
withElements  // Elementを内包していそう
closeable     // インターフェイス的に見える

// GOOD
isEmpty
hasElements
canClose
```
#### 名前付き引数にboolがある場合、形容詞や名刺を優先してつけ、動詞は避けるべき
#### bool値の命名には、ポジティブ表現を用いることを推奨します
```dart
// BAD
if (!socket.isDisconnected && !database.isEmpty) {
  socket.write(database.read());
}

// GOOD
if (socket.isConnected && database.hasData) {
  socket.write(database.read());
}
```
#### 外部に対して動作をしたり、状態を変える場合の命名は命令形を推奨します
#### 値を返す関数やメソッドの場合は、名詞や命令形でない動詞を推奨します
#### 機能やメソッドに注目させたい場合、命令形を推奨します
```dart
// GOOD
var table = database.downloadData();
var packageVersions = packageGraph.solveConstraints();
```
#### メソッド名を`get`で始めるのは避けましょう
#### オブジェクトの状態を引き渡すメソッドの場合、`to___()`と命名しましょう
```dart
list.toSet();
stackTrace.toString();
dateTime.toLocal();
```
#### オブジェクトが元のメソッドと別の状態を返す場合、`as___()`と命名しましょう
```dart
var map = table.asMap();
var list = bytes.asFloat32List();
var future = subscription.asFuture();
```
#### メソッドのパラメーターを命名に組み込むことは避けましょう
```dart
// BAD
list.addElement(element)
map.removeKey(key)

// GOOD
list.add(element);
map.remove(key);
```
#### 慣例的なものがある場合、1文字の命名に従いましょう。
```dart
// GOOD
class Map<K, V> {}
class Multimap<K, V> {}
class MapEntry<K, V> {}

class Future<T> {
  Future<S> then<S>(FutureOr<S> onValue(T value)) => ...
}
```

### ライブラリ
#### 変数やメソッドはプライベート宣言を優先してください
#### 同じライブラリに複数のクラスを宣言するようにしてください

### Class and mixins
#### 抽象クラス（abstract）を定義する場合、その型は1文字の命名をするのは避けましょう
#### 静的（static）のみしかないクラスの定義は避けましょう
```dart
// BAD
class DateUtils {
  static DateTime mostRecent(List<DateTime> dates) {
    return dates.reduce((a, b) => a.isAfter(b) ? a : b);
  }
}

class _Favorites {
  static const mammal = 'weasel';
}

// GOOD
DateTime mostRecent(List<DateTime> dates) {
  return dates.reduce((a, b) => a.isAfter(b) ? a : b);
}

const _favoriteMammal = 'weasel';
```
ただし、emunの様な扱いをする場合は例外です。
```dart
// GOOD
class Color {
  static const red = '#f00';
  static const green = '#0f0';
  static const blue = '#00f';
  static const black = '#000';
  static const white = '#fff';
}
```

#### 継承される予定のないクラスを継承するのは避けましょう
#### クラスが拡張を前提としているかドキュメント（コメント等）に残しましょう
#### インターフェイスとして用いる前提のないクラスを用いるのは避けましょう
#### インターフェイスとして実装する前提のクラスの場合、ドキュメント（コメント等）に残しましょう
#### mixin型を定義する場合は、`mixin`を用いましょう
#### mixinを意図していない型のものを混在させるのは避けましょう
#### nullableの場合、Future, Stream, Collection型をreturnすることは避けましょう
#### 

### Constructors
#### サポートされている場合、コンストラクタをconstにするようにしてください

### Members
#### フィールドとトップレベル変数をfinalにすることを推奨します
#### 概念的にプロパティにアクセスする操作には、ゲッターを使用すること
#### 概念的にプロパティを変更する操作には、セッターを使用すること
#### 対応するゲッターを持たずにセッターを定義しないでください
#### オーバーロードを装うために実行時の型テストを使用するのは避けてください
#### 初期化なしで`late final`で定義をしないでください
#### 複数メソッドを実行する場合、カスケードを用いましょう
```dart
// BAD
var buffer = StringBuffer()
    .write('one')
    .write('two')
    .write('three');
    
// GOOD
var buffer = StringBuffer()
  ..write('one')
  ..write('two')
  ..write('three');
```

### Types（データの型）
#### 初期値を持たない場合でも、`var`ではなく型を用いて定義しましょう
#### 明確でない場合、型定義をすること
#### 冗長な型定義は避けましょう
```dart
// BAD
List<List<Ingredient>> desserts = <List<Ingredient>>[];

// GOOD
var desserts = <List<Ingredient>>[];
```
#### 関数を定義する場合、returnされる型を定義しましょう
#### 関数のパラメーターにも型定義をしましょう
#### `map()`や`filter()`関数の引数では型定義をしてはいけません
```dart
// BAD
var names = people.map((Person person) => person.name);

// GOOD
var names = people.map((person) => person.name);
```
#### コンストラクタの`this.`に対して型定義をしてはいけません
#### 明確に判別できない場合、型定義をしましょう
#### 型の推測が容易にできる場合、型定義は冗長のためやめましょう
```dart
// BAD
class Downloader {
  final Completer<String> response = Completer<String>();
}

// GOOD
class Downloader {
  final Completer<String> response = Completer();
}
```
#### 抽象的すぎて不完全な型定義は避けましょう
```dart
// BAD
var completer = Completer<Map>();

// GOOD
var completer = Completer<Map<String, int>>();
```
#### 型の定義ができない、困難な場合でも`dynamic`型を記述しましょう
#### 関数の場合でも、詳細に型を定義しましょう
```dart
// BAD
bool isValid(String value, Function test) => ...

// GOOD
bool isValid(String value, bool Function(String) test) => ...
```
#### `setter`に戻り値の型を定義しないでください
#### `typedef`の使用はしないでください
#### 関数の型定義をする場合、引数に定義する方を優先しましょう
```dart
Iterable<T> where(bool predicate(T element)) => ...

// BETTER
Iterable<T> where(bool Function(T) predicate) => ...
```
#### 静的解析を無効にしない限り、`dynamic`型の使用は避けましょう
#### 値を生成しない非同期（Future）の場合、`void`を定義してください
#### 非同期関数の返り値の型定義に`FutureOr<T>`のように定義することは避けましょう

### Parameters（引数）


### Equality（イコール記号）
