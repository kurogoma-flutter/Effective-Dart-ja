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

### Constructors

### Error handling

### Asynchrony（非同期）

# 設計
### 命名

### ライブラリ

### Class and mixins

### Constructors

### Members

### Types（データの型）

### Parameters（引数）

### Equality（イコール記号）
