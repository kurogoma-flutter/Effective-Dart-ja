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
### １行コメント

### Doc（複数行）コメント

### マークダウン

### 記述方法

# 使用例
### ライブラリ

### null

### String

### Collections

### Functions

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
