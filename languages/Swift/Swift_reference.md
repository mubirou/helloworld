# <b>Swift 基礎文法</b>

### <b>INDEX</b>

* Hello,world! （[Linux](https://github.com/mubirou/HelloWorld/blob/master/languages/Swift/Swift_linux.md) / [macOS](https://github.com/mubirou/HelloWorld/blob/master/languages/Swift/Swift_mac.md) / [Windows](https://github.com/mubirou/HelloWorld/blob/master/languages/Swift/Swift_win.md)）
* [データ型](#データ型)
* [データ型の操作](#データ型の操作)
* [クラス](#クラス)
* [スーパークラスとサブクラス](#スーパークラスとサブクラス)
* [名前空間](#名前空間)
* [継承と委譲](#継承と委譲)
* [変数とスコープ](#変数とスコープ)
* [アクセサ （getter / setter）](#アクセサ)
* [演算子](#演算子)
* [定数](#定数)
* [メソッド](#メソッド)
* [匿名関数（クロージャ）](#匿名関数（クロージャ）)
* [クラス定数･変数･メソッド](#クラス定数･変数･メソッド)
* [if 文](#if文)
* [三項演算子](#三項演算子)
* [switch 文](#switch文)
* [for 文](#for文)
* [for...in 文](#for...in文)
* [while 文](#while文)
* [配列](#配列)
* [辞書（Dictionary）](#辞書（Dictionary）)
* [self](#self)
* [文字列の操作](#文字列の操作)
* [インターフェース（protocol）](#インターフェース（protocol）)
* [抽象クラス](#抽象クラス)
* [super](#super)
* [オーバーライド](#オーバーライド)
* [カスタムイベント](#カスタムイベント)
* [数学関数](#数学関数)


<a name="データ型"></a>
# <b>データ型</b>

### データ型の種類
1. 論理型 : Bool 型（他に Boolean 型あり）
1. 整数型 : Int 型（-9223372036854775808〜9223372036854775807）
1. 浮動小数点数型 : Float 型（小数点第5位までの値）
1. 浮動小数点数型 : Double 型（小数点第14位までの値）←デフォルト
1. 文字型 : Character 型
1. 文字型 : String 型 ←デフォルト
1. 列挙型
1. クラス
1. 配列 : Array 型
1. 辞書 : Dictionary 型
* 型指定に「?」（「!」と併用も）を付けることで「nil」の代入を許可する Optional 型に
* Any 型もあり

### 例文
```
//test.swift

//①論理型 : Bool型（他にBoolean型あり）
var _bool: Bool = true
print(_bool, type(of: _bool)) //=> true Bool

//②整数型 : Int型（-9223372036854775808〜9223372036854775807）
var _int: Int = 9223372036854775807 //約900京
print(type(of: _int)) //=> Int

//②浮動小数点数型 : Float型（小数点第5位までの値）
var _float: Float = 3.1415926535897932384626433832795
print(_float, type(of: _float)) //=> 3.14159  Float

//④浮動小数点数型 : Double型（小数点第14位までの値）←デフォルト
var _double: Double = 3.1415926535897932384626433832795
print(_double, type(of: _double)) //=> 3.14159265358979  Double

//⑤文字型 : Character型
var _char: Character = "a" //シングルクォーテーションは不可
print(_char, type(of: _char)) //=> "a"  Character

//⑥文字型 : String型 ←デフォルト
var _string: String = "007"
print(_string, type(of: _string)) //=> "007"  String

//⑦列挙型
enum Signal { case BLUE,YELLOW,Red }
print(Signal.BLUE) //=> BLUE

//⑧クラス
class MyClass {}
var _myClass: MyClass = MyClass()
print(_myClass, type(of: _myClass)) //=> test.MyClass MyClass

//⑪配列 : Array型
var _array: Array<String> = ["A","B","C"] //<Any>、<AnyObject>等も可
print(_array, type(of: _array)) //=> ["A","B","C"]  Array<String>

//⑫辞書 : Dictionary型
var _dic: Dictionary<String, String> = ["a":"あ", "i":"い", "u":"う"]
print(_dic, type(of: _dic)) //=> ["u": "う", "a": "あ", "i": "い"]  Dictionary<String, String>
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月13日  
更新日：2017年04月13日


<a name="データ型の操作"></a>
# <b>データ型の操作</b>

### データ型の調べ方
1. type(of:)
    ```
    //test.swift
    class MyClass {}
    var _myClass: MyClass = MyClass()
    print(type(of: _myClass)) //=> MyClass
    print(type(of: 99)) //=> Int
    ```

1.  is演算子
    * 他にも as 演算子（型キャスト）や as? 演算子（不可の場合 nil が返る）あり
    ```
    //test.swift
    class SuperClass {}
    class SubClass: SuperClass {}
    var _subClass: Any = SubClass() //「: SubClass」とすると以下でwarning
    print(_subClass is SubClass) //=> true
    print(_subClass is SuperClass) //=> true
    ```

1. キャスト（Int 型→ Bool 型）
    ```
    //test.swift
    var _int: Int = 1
    var _bool: Bool = (_int != 0) //0をfalseに変換（0以外はtrueに変換）
    print(_bool) //=> true
    ```

1. キャスト（Bool 型→ Int 型）
    ```
    //test.swift
    var _bool: Bool = true
    var _int: Int = _bool ? 1 : 0 //三項演算子を活用
    print(_int) //=> 1
    ```

1. キャスト（String 型→ Int 型）
    ```
    //test.swift
    var _string: String = "007"
    var _int: Int = Int(_string)! //「!」を付けないとOptional型になってしまう
    print(_int + 3) //=> 10
    ```

1. キャスト（Int 型→ String 型）
    ```
    //test.swift
    var _int: Int = 100;
    var _string: String = String(_int); //100（Int型）→"100"（String）に変換
    print(_string); //=> "100"
    print(type(of: _string)); //=> String
    ```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月26日  
更新日：2017年04月13日


<a name="クラス"></a>
# <b>クラス</b>

```
//test.swift
public class Rectangle { //長方形クラス ←アクセス修飾子を省略でinternal扱い
    private var _width: Int = 0 //インスタンス変数（プロパティ）
    private var _height: Int = 0 //インスタンス変数（プロパティ）

    init() { } //コンストラクタ
    
    //アクセサ
    public var width: Int {
        get { return _width }
        set { _width = newValue } //newValueは決め打ち
    }
    public var height: Int {
        get { return _height }
        set { _height = newValue } //newValueは決め打ち
    }

    //メソッド
    public func getArea() -> Int { //面積を計算して値を返す（返り値が無い場合->は不要）
        return _width * _height
    }
}

//①インタンスの生成
var _rectangle: Rectangle = Rectangle()

//②フィールドの更新
_rectangle.width = 1920
_rectangle.height = 1080

//③フィールドの取得
print(_rectangle.width) //=> 1920
print(_rectangle.height) //=> 1080

//④メソッドの実行
print(_rectangle.getArea()) //=> 2073600
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月26日  
更新日：2017年04月13日


<a name="スーパークラスとサブクラス"></a>
# <b>スーパークラスとサブクラス</b>
* 多重継承は不可
* デフォルトのアクセス修飾子は internal（同一プロジェクト内でアクセス可）

### 例文
```
//test.swift
//スーパークラス（internalは省略可能）
internal class SuperClass { 
    private var _fieldS: String  = "スーパークラスのプロパティ" //①インスタンス変数
    internal var fieldS: String  { get { return _fieldS }} //②アクセサ（getter）
    internal func methodS() -> String { return "スーパークラスのメソッド" } //③メソッド        
}

//サブクラスＡ（internalは省略可能／多重継承不可）
internal class SubClassA : SuperClass {
    private var _fieldA: String  = "サブクラスＡのプロパティ" //①インスタンス変数
    internal var fieldA: String  { get { return _fieldA }} //②アクセサ（getter）
    internal func methodA() -> String { return "サブクラスＡのメソッド" } //③メソッド
}

//サブクラスＢ（internalは省略可能／多重継承不可）
internal class SubClassB : SuperClass { 
    private var _fieldB: String  = "サブクラスＢのプロパティ" //①インスタンス変数
    internal var fieldB: String  { get { return _fieldB }} //②アクセサ（getter）
    internal func methodB() -> String { return "サブクラスＢのメソッド" } //③メソッド
}

// 実行
var _subclassA:SubClassA = SubClassA();
print(_subclassA.fieldS); //=> "スーパークラスのプロパティ"
print(_subclassA.fieldA); //=> "サブクラスＡのプロパティ"
print(_subclassA.methodS()); //=> "スーパークラスのメソッド"
print(_subclassA.methodA()); //=> "サブクラスＡのメソッド"

var _subclassB:SubClassB = SubClassB();
print(_subclassB.fieldS); //=> "スーパークラスのプロパティ"
print(_subclassB.fieldB); //=> "サブクラスＢのプロパティ"
print(_subclassB.methodS()); //=> "スーパークラスのメソッド"
print(_subclassB.methodB()); //=> "サブクラスＢのメソッド"
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月26日  
更新日：2017年04月13日


<a name="名前空間"></a>
# <b>名前空間</b>

### 概要
* Swift の名前空間には次の２種類ある
    1. Nested Types : クラスのネストによる方法
    1. module : UIKit や Foundation といったフレームワークの利用

### 例文（Nested Typesによる名前空間）
```
//test.swift
class MyLibrary {
    class MyClass {
        private var _w: Int
        private var _h: Int
        init(width _w: Int=640, height _h: Int=480) {
            self._w = _w
            self._h = _h
        }
        var width: Int {
            get { return _w }
            set { _w = newValue }
        }
        var height: Int {
            get { return _h }
            set { _h = newValue }
        }
    }
    class MyClass2 {
        //いろいろな機能
    }
}

var _myClass: MyLibrary.MyClass = MyLibrary.MyClass()
print(_myClass.width, _myClass.height) //=> 640 480

var _myClass2: MyLibrary.MyClass2 = MyLibrary.MyClass2()
print(_myClass2) //=> test.MyLibrary.MyClass2
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月29日  
更新日：2017年04月13日


<a name="継承と委譲"></a>
# <b>継承と委譲</b>

### 概要
* GoF デザインパターンの [Adapter パターン](http://bit.ly/2naab8x)等で利用される
* 継承の場合は「: クラス名」を使い、委譲の場合は「クラス名()」を使ってオブジェクトを生成し、他のクラスの機能を利用する

### 継承版
```
//test.swift
internal class ClassA { //internalは省略可
    internal func myMethod() { //internalは省略可
        print("ClassA.myMethod()")
    }
}

internal class ClassB : ClassA {} //ClassAを継承

var _classB: ClassB = ClassB();
_classB.myMethod(); //=> "ClassA.myMethod()"
```

### 委譲版
```
//test.swift
internal class ClassA { //internalは省略可
    internal func myMethod() { //internalは省略可
        print("ClassA.myMethod()")
    }
}

internal class ClassB { //この内容だけが継承版と異なる
    private var _classA:ClassA; //プロパティにインスタンスを格納（委譲）
    init() { //コンストラクタ
        _classA = ClassA(); //プロパティにインスタンスを格納
    }
    internal func myMethod() { //internalは省略可
        _classA.myMethod();
    }
}

var _classB:ClassB = ClassB();
_classB.myMethod(); //=> "ClassA.myMethod()"
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月26日  
更新日：2017年04月13日


<a name="変数とスコープ"></a>
# <b>変数とスコープ</b>

### 変数の種類
1. インスタンス変数
    * open : 別のモジュールからもアクセス可（旧 public と同等）
    * public : 別のモジュールからもアクセス可（但し継承・オーバーライドは不可）
    * internal : 同じモジュール内からのみアクセスできる ←デフォルト
    * fileprivate : 同じソースファイル内からのみアクセスできる（旧 private と同等）
    * private : 定義されたスコープ内でのみアクセスできる

1. ローカル変数
    * メソッド内 : メソッド内でのみアクセス可
    * 引数 : メソッド内でのみアクセス可
    * for 文 : for 文内でのみアクセス可

1. グローバル変数 : ソースファイル内のどこからでもアクセス可

1. クラス変数（静的変数）

### public（インスタンス変数）: 非推奨
```
//test.swift
public class MyClass { //internal（省略可）は不可
    public var _p: String = "ほげ" //public宣言
}
var _myClass: MyClass = MyClass()
print(_myClass._p) //=> "ほげ" //参照可（他人の変数を勝手にいじる行為）
_myClass._p = "ほげほげ" //変更可（他人の変数を勝手にいじる行為）
print(_myClass._p) //=> "ほげほげ"
```

### internal（インスタンス変数）: 非推奨（デフォルト）
```
//test.swift
internal class MyClass { //internalは省略可
    internal var _p: String = "ほげ" //internalは省略可
}
var _myClass: MyClass = MyClass()
print(_myClass._p) //=> "ほげ" //参照可（他人の変数を勝手にいじる行為）
_myClass._p = "ほげほげ" //変更可（他人の変数を勝手にいじる行為）
print(_myClass._p) //=> "ほげほげ"
```

### private（インスタンス変数）: 推奨
```
//test.swift
internal class MyClass { //internalは省略可
    private var _p: String = "ほげ" //private宣言
    internal var p: String { //_pのアクセサ ←internalは省略可
        get { return _p }
        set { _p = newValue }
    }
}
var _myClass: MyClass = MyClass()
print(_myClass.p) //=> "ほげ" ←getterで参照
_myClass.p = "ほげほげ" //setterで変更
print(_myClass.p) //=> "ほげほげ"
```

### ローカ変数
1. メソッド内で宣言する場合
    ```
    //test.swift
    class MyClass { //internal扱い
        private var _v: String = "PRIVATE"; //private宣言
        init() {
            print(_v) //=> "PRIVATE"
        }
        func myMethod() -> Void { // -> Void は省略可
            var _v: String //内部変数（≒ローカル変数）宣言のみ ←設定は不可
            _v = "LOCAL" //ローカル変数への値の設定
            print(_v) //=> "LOCAL"
            print(self._v) //=> "PRIVATE"
        }
    }
    var _myClass: MyClass = MyClass()
    _myClass.myMethod()
    ```

1. 引数として利用する場合
    ```
    //test.swift
    class MyClass { //internal扱い
        private var _name: String = "TARO"; //private宣言
        init() {
            print(_name) //=> "TARO"
        }
        func myMethod(_name: String) -> Void { // -> Void は省略可
            print(_name) //=> "HANAKO"
            print(self._name) //=> "TARO" ←インスタンス変数の参照はselfが必要
        }
    }
    var _myClass: MyClass = MyClass()
    _myClass.myMethod(_name:"HANAKO") //引数の渡し方が独特
    ```

1. for 文内で宣言する場合
    ```
    //test.swift
    class MyClass { //internal扱い
        private var _i:Int = 999; //private宣言
        init() {
            print(_i) //=> 999
        }
        func myMethod() -> Void { // -> Void は省略可
            for _i in 0..<10 {
                print(_i); //=> 0、1、2、…、9
                print(self._i); //=> 999
            }
            print(_i); //=> 999
        }
    }
    var _myClass: MyClass = MyClass()
    _myClass.myMethod()
    ```

### グローバル変数
```
//test.swift
var _global: String = "GLOBAL"

//==================================
// メソッド内のグローバル変数の扱い
//==================================
func myMethod() -> Void { // -> Void は省略可
    print(_global) //=> "GLOBAL" ←何も宣言することなく利用可能
}
myMethod()

//================================
// クラス内のグローバル変数の扱い
//================================
class MyClass { //internal扱い
    init() {
        print(_global) //=> "GLOBAL" ←何も宣言することなく利用可能
    }
}
var _myClass: MyClass = MyClass()
```

### クラス変数（静的変数）
```
//test.swift
class MyMath { //internal扱い
    internal static var PI: Double = 3.14159265358979 //internalは省略可
}
print(MyMath.PI) //=> 3.14159265358979
MyMath.PI = 3.14 //変更可能
print(MyMath.PI) //=> 3.14
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月27日  
更新日：2017年04月13日


<a name="アクセサ"></a>
# <b>アクセサ （getter / setter）</b>

### 読み書き可能なプロパティ
```
//test.swift
internal class Nishimura { //internalは省略可
    private var _age: Int = 49 //private宣言
    //アクセサ
    internal var age: Int {
        get {
            return _age
        }
        set {
            _age = newValue
        }
    }
}

var _nishimura: Nishimura = Nishimura()
print(_nishimura.age) //=> 49 ←getter
//print(_nishimura._age) //error（直接のアクセス不可）
_nishimura.age = 50 //変更可能 ←setter
print(_nishimura.age) //=> 50 ←getter
```

#### 読み取り専用のメンバ変数
```
//test.swift
internal class Nishimura { //internalは省略可
    private var _age: Int = 49 //private宣言
    //アクセサ
    internal var age: Int {
        get {
            return _age
        }
    }
}

var _nishimura: Nishimura = Nishimura()
print(_nishimura.age) //=> 49 ←getter
//print(_nishimura._age) //error（直接のアクセス不可）
//_nishimura.age = 50 //=> error ←変更できません
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月27日  
更新日：2017年04月14日


<a name="演算子"></a>
# <b>演算子</b>

### 算術演算子
* 複合代入演算子 +=, -=, *=, /=, %= などあり
```
//test.swift
print(3 + 2); //=> 5 (可算)
print(5 - 8); //=> -3 (減算)
print(3 * 4); //=> 12 (乗算)
print(1 + 2 * 3 - 4 / 2); //=> 5 (複雑な計算)
print(63 % 60); //=> 3 (余剰)
print(8 / 3); //=> 2(除算) ←整数の場合、余りは切り捨てられる
print(8.0 / 3); //=> 2.66666666666667（小数点第14位まで）
```

### インクリメント、デクリメントの廃止
* バージョン3.0からインクリメントおよびデクリメントは廃止
```
//test.swift
var hoge_: Int = 0
hoge_ += 1 //複合代入演算子（+=、-=）で代用
print(hoge_) //=> 1
```

### その他の演算子
```
//test.swift
print(true && true); //=> true（論理積）
print(true || false); //=> true（論理和）
print(!true); //=> false（否定）←スペースを空けるとerror（要注意）

print(2 < 3); //=> true（比較/未満）
print(2 <= 2); //=> true（比較/以下）
print(1 == 1.0); //=> true（等号）
print(1 != 1.0); //=> false（不等号）
//同じインスタンスか否かを調べる場合「===」「!==」を使用します。

print(3 & 1); //=> 1（ビット積）
print(3 | 1); //=> 3（ビット和）
print(3 ^ 1); //=> 2（排他的ビット和）
print(2 << 7); //=> 256（ビット･シフト）
print(~3); //=> -4（ビット反転）
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月27日  
更新日：2017年04月14日


<a name="定数"></a>
# <b>定数</b>

### 概要
* 値の「変更がある」変数は「var」を付けて宣言
* 値の「変更がない」変数は「let」を付けて宣言

### 通常の定数
* 構文
```
let 定数名: 型 = 値
```

* 例文
```
//test.swift
let PI:Double = 3.1415926535897932384626433832795
print(PI); //=> 3.14159265358979
//PI = 3.14 //=> error ←変更は不可
```

### クラス定数（静的定数）
* 構文
```
//test.swift
internal class クラス名 { //internalは省略可
    internal static let 定数名: データ型 = 値 //「internal」「public」にする
        ………
}

//アクセス方法
クラス名.定数名
```

* 例文
```
//test.swift
internal class MyMath { //internalは省略可
    internal static let PI:Double = 3.14159265358979 //internalは省略可
}

print(MyMath.PI) //=> 3.14159265358979 ←インスタンスの生成が不要
//MyMath.PI = 3.14 //変更不可
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月27日  
更新日：2017年04月14日


<a name="メソッド"></a>
# <b>メソッド</b>

### 基本構文
```
[アクセス修飾子] [static] func メソッド名([引数:型, …]) -> 戻り値の型 {
    [return 戻り値]
}
//static はクラスメソッド（静的メソッド）
```

* アクセス修飾子
    * open : 別のモジュールからもアクセス可（旧 public と同等）
    * public : 別のモジュールからもアクセス可（但し継承・オーバーライドは不可）
    * internal : 同じモジュール内からのみアクセスできる ←デフォルト
    * fileprivate : 同じソースファイル内からのみアクセスできる（旧 private と同等）
    * private : 定義されたスコープ内でのみアクセスできる

### 基本例文
```
//test.swift
internal class MyClass { //internalは省略可
    //○〜○までの値を足した合計を返す
    internal func tashizan(_start:Int, _end:Int) -> Int { //internalは省略可
        var _result:Int //ローカル変数（内部変数）の宣言
        _result = 0; //ローカル変数の初期化
        for i in _start..<_end+1 { //..<の間をあけるとerror
            _result += i;
        }
        return _result;
    }
}

var _myClass: MyClass = MyClass();
print(_myClass.tashizan(_start:1, _end:10)); //=> 55
print(_myClass.tashizan(_start:1, _end:100)); //=> 5050
```

### コンストラクタ＝イニシャライザ
* 引数ありと引数なしを同時に定義するとが可能）
```
//test.swift
internal class MyClass { //internalは省略可
    //引数なしのコンストラクタの宣言
    init() { 
        print("インスタンスが生成")
    }
    //引数ありのコンストラクタの宣言
    init(arg1: String) {
        print("インスタンスが生成:" + arg1)
    }
}

var _myClass1: MyClass = MyClass() //=> "インスタンスが生成"
var _myClass2: MyClass = MyClass(arg1:"引数あり") //=> "インスタンスが生成:引数あり"
```

### クラスメソッド＝静的メソッド
```
//test.swift
internal class MyMath { //internalは省略可
    internal static func pow(arg1:Int, arg2:Int) -> Int { //internalは省略可
        if (arg2 == 0) { return 1 } //0乗対策
        var _result:Int //ローカル変数宣言
        _result = arg1 //ローカル変数の初期化
        for i in 1..<arg2 {
            if i == 0 { return 0 } //iを使わないとerrorになるので…
            _result = _result * arg1
        }
        return _result;
    }
}

print(MyMath.pow(arg1:2, arg2:0)); //=> 1（2の0乗）
print(MyMath.pow(arg1:2, arg2:1)); //=> 2（2の1乗）
print(MyMath.pow(arg1:2, arg2:8)); //=> 256（2の8乗）
```

### デフォルト値付き引数
```
//test.swift
internal class MyClass { //internalは省略可
    private var _point: Int = 0
    internal func addPoint(_point:Int=1) -> Void { // -> Void は省略可
        self._point += _point
        print(self._point)
    }
}

var _myClass:MyClass = MyClass()
_myClass.addPoint() //=> 1
_myClass.addPoint(_point:10) //=> 11
```

### 可変長引数
```
//test.swift
internal class MyClass { //internalは省略可
    internal func sum(_points:Int...) -> Void { // -> Void は省略可
        var _result:Int //ローカル変数宣言
        _result = 0
        for tmp in _points { //引数は配列（Array）
            _result += tmp
        }
        print(_result)
    }
}

var _myClass:MyClass = MyClass()
_myClass.sum(_points:1,1) //=> 2（1+1）
_myClass.sum(_points:1,2,3,4,5); //=> 15（1+2+3+4+5）←引数の数はいくつでも可
```

### 名前付き引数（引数名の指定の簡略化が可能）
```
//test.swift
internal class MyClass { //internalは省略可
    internal func myMethod(name _newUserName: String) -> Void { // -> Void は省略可
        print(_newUserName)
    }
}

var _myClass:MyClass = MyClass()
_myClass.myMethod(name:"CHIKASHI") //=> "CHIKASHI"
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月27日  
更新日：2017年04月14日


<a name="匿名関数（クロージャ）"></a>
# <b>匿名関数（クロージャ）</b>

### 構文
```
[アクセス修飾子] var 変数名 = { ([引数:型, …]) -> 戻り値の型 in
    ………
}
```
* 内容を変更させたくない場合は var ではなく let にする
* デフォルト値付き引数は利用不可
* インスタンス変数としても利用可能

### 例文
```
//test.swift
//無名関数①（オリジナル）
var _hello = { (_name: String) -> String in
    return _name + "," + "Hello"
}

//無名関数②（入替用）
var _japaneseHello = { (_name: String) -> String in
    return _name + "、" + "こんにちは"
}

//無名関数③（入替用）
var _chineseHello = { (_name: String) -> String in
    return _name + "," + "你好"
}

//無名関数①の実行
print(_hello("CHIKASHI")) //=> "CHIKASHI,Hello" ←_hello(_name:"CHIKASHI")ではない

//無名関数②に入替えて実行
_hello = _japaneseHello
print(_hello("CHIKASHI")) //=> "CHIKASHI、こんにちは" ←_hello(_name:"CHIKASHI")ではない

//無名関数③に入替えて実行
_hello = _chineseHello
print(_hello("CHIKASHI")) //=> "CHIKASHI,你好" ←_hello(_name:"CHIKASHI")ではない
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月27日  
更新日：2017年04月14日


<a name="クラス定数･変数･メソッド"></a>
# <b>クラス定数･変数･メソッド</b>
* 静的メンバはクラスをインスタンス化せずにアクセスが可能

```
//test.swift
internal class MyMath { //internalは省略可
    //クラス定数（静的定数）
    internal static let PI: Double = 3.14159265358979 //internalは省略可
    
    //クラス変数（静的変数）
    internal static var lastUpdate: String = "2016-07-27" //internalは省略可
    
    //クラスメソッド（静的メソッド）
    internal static func pow(arg1:Int, arg2:Int) -> Int { //internalは省略可
        if (arg2 == 0) { return 1 } //0乗対策
        var _result: Int //ローカル変数宣言
        _result = arg1 //ローカル変数の初期化
        for i in 1..<arg2 {
            if i == 0 { return 0 } //iを使わないとerrorになるので…
            _result = _result * arg1
        }
        return _result
    }
}

//クラス定数（静的定数）
print(MyMath.PI) //=> 3.14159265358979
//MyMath.PI = 3.14 //error ←変更不可

//クラス変数（静的変数）
print(MyMath.lastUpdate) //=> "2016-07-27"
MyMath.lastUpdate = "2017-04-14" //変更可能
print(MyMath.lastUpdate) //=> "2017-04-14"

//静的メソッドの実行
print(MyMath.pow(arg1:2, arg2:0)) //=> 1（2の0乗）
print(MyMath.pow(arg1:2, arg2:1)) //=> 2（2の1乗）
print(MyMath.pow(arg1:2, arg2:8)) //=> 256（2の8乗）
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月27日  
更新日：2017年04月14日


<a name="if文"></a>
# <b>if 文</b>

### 基本例文
* true と評価される可能性が高い順に並べると if 文を早く抜け出せる可能性が高い
```
//test.swift
var age_:Int = 49
if (age_ <= 20) { // () は省略可
    print("20歳以下")
} else if (age_ <= 40) {
    print("21〜40歳")
} else if (age_ <= 60) {
    print("41〜60歳") //これが出力される
} else {
    print("61歳以上")
}
```

### 論理積（AND）
1. 論理演算子（&&）を使う方法
    ```
    if (条件式① && 条件②) {
        処理A ←条件式① かつ 条件式② の両方がtrueの場合に実行
    } else {
        処理B
    }
    ```
1. if のネストを使う方法
    ```
    if (条件式①) {
        if (条件②) {
            処理A ←条件式① かつ 条件式② の両方がtrueの場合に実行
        } else {
            処理B
        }
    } else {
        処理B
    }
    ```

### 論理和（OR）
1. 論理演算子（||）を使う方法
    ```
    if (条件式① || 条件②) {
        処理A ←条件式①または条件式②の両方がtrueの場合に実行
    } else {
        処理B
    }
    ```

1. ifのネストを使う方法
    ```
    if (条件式①) {
        処理A ←条件式①がtrueの場合に実行
    } else if (条件②) {
        処理A ←条件式②がtrueの場合に実行
    } else {
        処理B
    }
    ```

### 排他的論理和（XOR）
```
//test.swift
var _a: Bool = true
var _b: Bool = false
if ((_a || _b) && !(_a && _b)) {
    print("どちらか一方だけtrueです");
} else {
    print("両方共にtrueかfalseです");
}
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="三項演算子"></a>
# <b>三項演算子</b>

### 比較式が１つの場合
```
//test.swift
var age_:Int = 49
var _result: String = (age_ < 60) ? "現役" : "退職"
print(_result); //=> "現役"
```

### 三項演算子（比較式が複数の場合）
```
//test.swift
var age_:Int = 49
var _result: String = 
(age_ < 20) ? "未成年":
(age_ < 60) ? "現役":
"退職"
print(_result) //=> "現役"
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="switch文"></a>
# <b>switch 文</b>
* 他の多くの言語とは異なり各処理の後の break 文は不要

### 基本構文
```
switch 式 {
    case 式① : 式と式①が等しいときの処理
    case 式② : 式と式②が等しいときの処理
    default : それ以外のときの処理
}
```

### 判別式が Bool 型の場合
```
//test.swift
var age_: Int = 49
switch (true) {
    case age_ <= 20: print("20歳以下")
    case age_ <= 60: print("21〜60歳") //これが出力される
    default: print("61歳以上")
}
```

### 判別式が Bool 型ではない場合
```
//test.swift
var _name: String = "CHIKASHI"
switch (_name) {
    case "CHIKASHI": print("父") //これが出力
    case "HANAKO": print("母")
    case "TARO": print("長男")
    case "JIRO": print("次男")
    default: print("家族以外")
}
```

### fallthrouh（フォールスルー）
```
var _name: String = "TARO"
switch (_name) {
    case "CHIKASHI": fallthrough //ここで終了せず次のcaseの処理へ
    case "HANAKO": print("親")
    case "TARO": fallthrough //ここで終了せず次のcaseの処理へ
    case "JIRO": print("子") //これが出力
    default: print("家族以外")
}
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="for文"></a>
# <b>for 文</b>

### 基本構文
```
for ループ制御変数 in 開始 ..< 終了 { //終了は含みません
    繰り返す処理
}
```

### 基本例文
```
//test.swift
for i in 0 ..< 10 { // ..< は空白を入れてはいけない
    print(i); //=> 0,1,2,3,4,5,6,7,8,9
}
//print(i); //error（for文の外では使えない）
```

### break 文
```
//test.swift
var _count: Int = 0
for i in 0 ..< 100000 { // ..< は空白を入れてはいけない
    _count += 1
    if (_count > 100) {
        break //ループを終了
    }
    print(_count) //=> 1,2,...,99,100
}
print("for文終了")
```

### continue 文
```
//test.swift
    for i in 0 ..< 20 { //iは1,2,...,18,19
        if ((i % 3) != 0) { //3で割って余りが0ではない（＝3の倍数ではない）場合
            continue; //for文の残処理をスキップしてfor文の次の反復を開始する
        }
        print(i) //=> 3,6,9,12,15,18 ←3の倍数
    }
print("for文終了")
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="for...in文"></a>
# <b>for...in 文</b>

### 基本構文
```
for 変数 in 配列等 {
    print(変数名)
}
```

### 配列（1次元）の場合
```
//test.swift
var _array:[String] = ["A","B","C"]
for value in _array {
    print(value) //=> "A"→"B"→"C"
}
```

### 配列（2次元）の場合
```
//test.swift
var _array:[[String]] = [
    ["x0y0","x1y0","x2y0"], //0行目
    ["x0y1","x1y1","x2y1"]  //1行目
]
for theArray in _array {
    for value in theArray {
        print(value)
        //=> "x0y0"→"x1y0"→"x2y0"→"x0y1"→"x1y1"→"x2y1"    
    }
}
```

### 辞書（Dictionary 型）の場合
```
//test.swift
var _dic:Dictionary<String,String> = ["A":"あ", "I":"い"]
for value in _dic {
    print(value.key + " : " + value.value)
    //=> "A : あ"
    //=> "I : い"
}
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="while文"></a>
# <b>while 文</b>

### while 文
```
//test.swift
var _i: Int = 0
while _i < 10 { //ループ判定式には条件式しか指定できません
    print(_i) //=> 0,1,2,3,4,5,6,7,8,9
    _i += 1
}
print(_i) //=> 10（変数はまだ有効）
```

### repeat...while 文 ≒ do...while 文
```
//test.swift
var _i: Int = 0
repeat {
    print(_i) //=> 0 ←ループ判定式はfalseだが１回実行される
    _i += 1
} while _i < 0
```

### break 文
```
//test.swift
var _count: Int = 0
while true { //ループ判別式をtrueにすると無限ループに!
    _count += 1
    if (_count > 100) {
        break //break文を使ってwhileループから抜け出て処理を終了
    }
    print(_count) //=> 1,2,....,99,100
}
print("while文終了")
```

### continue文
```
//test.swift
var _i: Int = 1;
while _i <= 20 {
    if ((_i % 3) != 0) { //3で割って余りが0ではない（＝3の倍数ではない）場合
        _i += 1
        continue //while文の残処理をスキップしてwhile文の次の反復を開始する
    }
    print(_i) //=> 3,6,9,12,15,18（3の倍数を出力）
    _i += 1
}
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="配列"></a>
# <b>配列</b>

### 作成と取得（1次元）
* 作成方法
```
var _array1: Array<String> = ["A","B","C"]
var _array2: [String] = ["A","B","C"]
var _array3: Array = ["A","B","C"] //型推論
```
* 例文
```
//test.swift
var _array:[String] = ["A","B","C"]
print(_array) //=> ["A", "B", "C"]
print(_array.dynamicType) //=> Array<String>
print(_array[0]) //=> "A" ←要素を取得（指定位置）する方法
```

### 作成と取得（2次元）
* 構文
```
var 変数名: [[データ型]] = [[○,○,...],[○,○,...],...]
```
* 例文
```
//test.swift（コインロッカーのようなイメージ）
var coinlocker_:[[String]] = [
    ["1083","7777","",""], //0行目
    ["","","",""],         //1行目
    ["","0135","",""],     //2行目
    ["","","",""],         //3行目
    ["","","","1234"]      //4行目
]
print(coinlocker_[0][0]); //=> "1083"
print(coinlocker_[0][1]); //=> "7777"
print(coinlocker_[2][1]); //=> "0135"
print(coinlocker_[4][3]); //=> "1234"
```

### 抽出（○番目から○番目）
* 構文
```
Array[開始インデックス番号...終了インデックス番号] //終了インデックス番号を含む
```
* 例文
```
//test.swift
var _array: [String] = ["A","B","C"]
print(_array[0...1]) //=> ["A","B"]
```

### 要素の数
```
//test.swift
var _array:[String] = ["A","B","C"]
for i in 0 ..< _array.count { //この場合要素の数は「3」
    print(_array[i]) //=> "A"→"B"→"C"
}
```

### 追加（最後）
* 構文
```
Array.append (値)
```
* 例文
```
//test.swift
//["A","B"]→["A","B","C"]
var _array: [String] = ["A","B"]
_array.append("C")
for value in _array {
    print(value) //=> "A"→"B"→"C"
}
```

### 追加（指定位置）
* 構文
```
Array.insert(値, at:インデックス番号) //先頭（0）〜最後（Array.count）まで指定可能
```
* 例文
```
//test.swift
//["A","B"]→["C","A","B"]
var _array:[String] = ["A","B"]
_array.insert("C", at:0)
for value in _array {
    print(value) //=> "C"→"A"→"B"
}
```

### 更新（任意の値）
* 構文
```
Array[インデックス番号] = 値
```
* 例文
```
//test.swift
//["A","B","C"]→["D","B","C"]
var _array:[String] = ["A","B","C"]
_array[0] = "D" //0番目を変更する場合
for value in _array {
    print(value) //=> "D"→"B"→"C"
}
```

### 更新（nil 型）
* 構文
```
var 変数:[データ型?] = [○,○,...]
変数[インデックス番号] = nil
```
* 例文
```
//test.swift
//[Optional("A"), Optional("B"), Optional("C")] → [nil,Optional("B"),Optional("C")]
var _array: [String?] = ["A", "B", "C"]
_array[0] = nil
print(_array[0...2]) //[nil, Optional("B"), Optional("C")]
```

### 削除（指定のインデックス）
* 構文
```
Array.remove(at:インデックス番号); //指定のインデックス番号の要素を削除
//先頭（0）〜最後（Array.count-1）まで指定可能
```
* 例文
```
//test.swift
//["A","B","C"]→["B","C"]
var _array:[String] = ["A","B","C"]
_array.remove(at:0) //先頭を削除する場合
for value in _array {
    print(value) //=> "B"→"C"
}
```

### 削除（最後）
* 構文
```
Array.removeLast()
```
* 例文
```
//test.swift
//["A","B","C"]→["A","B"]
var _array:[String] = ["A","B","C"]
_array.removeLast()
for value in _array {
    print(value) //=> "A"→"B"
}
```

### 結合
```
//test.swift
var _array1:[String] = ["A", "B"]
var _array2:[String] = ["C", "D"]
_array1 += _array2
print(_array1) //=> ["A", "B", "C", "D"]
```

### 複製
```
//test.swift
var _array1:[String] = ["A","B","C"]
var _array2:[String] = _array1 //代入は参照ではなく複製（注意）
_array2[0] = "X" //片方の配列の要素のみ変更してみる
print(_array1) //=> ["A","B","C"]
print(_array2) //=> ["X","B","C"] 
```

### 全要素を取り出す
1. for...in 文を使った例
    ```
    //test.swift
    var _array:[String] = ["A","B","C"]
    for value in _array {
        print(value) //=> "A"→"B"→"C"
    }
    ```

1. for 文を使った例
    ```
    //test.swift
    var _array:[String] = ["A","B","C"]
    for i in 0 ..< _array.count {
        print(_array[i]) //=> "A"→"B"→"C"
    }
    ```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="辞書（Dictionary）"></a>
# <b>辞書（Dictionary）</b>
* 辞書は「キー」と「値」の組み合わせを格納するデータ構造です

```
//test.swift
//①作成
var _dic: Dictionary<String, String> = ["A":"あ"]

//②追加
_dic["I"] = "い"
_dic["U"] = "う"

//③更新
_dic["I"] = "ゐ"

//④全てのデータを取得（その１）
for (key, value) in _dic {
    print(key, value) //=> U う → A あ → I ゐ
}

//④全てのデータを取得（その２）
for value in _dic {
    print(value.key, value.value) //=> U う → A あ → I ゐ
}

//確認
print(_dic) //=> ["U": "う", "A": "あ", "I": "ゐ"]
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="self"></a>
# <b>self</b>

### selfが必要な場合
1. 「引数」と「インスタンス変数」が同じ場合
1. 「ローカル変数」と「インスタンス変数」が同じ場合
* selfは、selfを記述したメソッドを所有するクラス（オブジェクト）を指す

### 例文
```
//test.swift
internal class Robot { //internalは省略可
    private var _x: Int //インスタンス変数（ここではselfは不可）
    
    init(_x: Int) { //引数
        self._x = _x //①selfが無いとerror
        print(self) //=> test.Robot（このメソッドが実行されたオブジェクト）
    }
    internal func move() -> Void { //internalは省略可
        var _x: Int //ローカル変数宣言
        _x = self._x + 10 //②selfが無いとerror
        if (_x >= 1920) {
            _x = 0
        }
        self._x = _x //②selfが無いとerror
        print(self) //=> test.Robot（このメソッドが実行されたオブジェクト）
    }
    internal var x: Int { //internalは省略可
        get { 
            return _x //selfを付けてもよい（通常は省略）
        }
    }
 }

var _robot:Robot = Robot(_x:500)
_robot.move()
print(_robot.x) //=> 510
//print(self) //=> error
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月28日  
更新日：2017年04月14日


<a name="文字列の操作"></a>
# <b>文字列の操作</b>

### String オブジェクトの作成
```
var 変数: String = String("○○")
var 変数: String = "○○"
```

### 長さを調べる（ダブルバイトにも対応）
```
○○.characters.count
```

### 一部分を取得
```
//test.swift
var _string: String = "0123456789"
var _start = _string.index(_string.startIndex, offsetBy:0) //最初から0文字目〜
var _end = _string.index(_string.startIndex, offsetBy:3) //最初から3文字目まで
var _result = _string[_start ... _end]
print(_result) //=> "0123"
```

### 一部分を取得（カスタム関数版）
```
//test.swift
//カスタム関数（前方宣言が必要）
func subString(string arg1: String, start arg2:Int, end arg3:Int) -> String {
    var _result: String
    _result = arg1[arg1.index(arg1.startIndex, offsetBy:arg2)
    ...
    arg1.index(arg1.startIndex, offsetBy:arg3)]
    return _result
}

var _string: String = "0123456789"
print(subString(string: _string, start:0, end:3)) //=> "0123"
print(subString(string: _string, start:2, end:5)) //=> "2345"
```

### 一部分を削除
```
//test.swift
var _string: String = "0123456789"
var _start = _string.index(_string.startIndex, offsetBy:0) //最初から0文字目〜
var _end = _string.index(_string.startIndex, offsetBy:3) //最初から3文字目まで
_string.removeSubrange(_start ..< _end)
print(_string) //=> "3456789"
```

### 一部分を削除（カスタム関数版）
```
//test.swift
//カスタム関数（前方宣言が必要）
func deleteString(string arg1: String, start arg2:Int, end arg3:Int) -> String {
    var _result: String
    _result = arg1
    _result.removeSubrange(_result.index(_result.startIndex, offsetBy:arg2) 
    ..< 
    _result.index(_result.startIndex, offsetBy:arg3))
    return _result
}

var _string: String = "0123456789"
print(deleteString(string: _string, start:0, end:3)) //=> "3456789"
print(deleteString(string: _string, start:2, end:5)) //=> "0156789"
```

### 置換
```
//test.swift
var _string: String = "2017年04月14日";
var _start = _string.index(_string.startIndex, offsetBy:0) //最初から0文字目〜
var _end = _string.index(_string.startIndex, offsetBy:4) //最初から4文字目まで
_string.replaceSubrange(_start ... _end, with:"平成29年")
print(_string) //=> "平成29年04月14日";
```

### 文字列→配列
* 構文
```
import Foundation
String.components(separatedBy:"区切り文字")
```

* 例文
```
//test.swift
import Foundation
var _string: String = "A,B,C,D" //「,」区切りの文字列
var _array = _string.components(separatedBy:",")
print(_array, type(of: _array)) //=> ["A", "B", "C", "D"] Array<String>
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月29日  
更新日：2017年04月14日


<a name="正規表現"></a>
# <b>正規表現</b>

* Java には以下のサンプル以外にも多くの正規表現の機能が用意されています

### 検索＆置換
```
//Main.java
import java.util.regex.*; //Pattern、Matcherに必要
public class Main { //public は省略可
    public static void main(String[] args) { //決め打ち(自動的に実行)
        String _string = "吉田松蔭,高杉晋作,久坂玄瑞,吉田稔麿,伊藤博文";
        String _result = "";
        String _regex = "吉田";

        Pattern _pattern = Pattern.compile(_regex);
        Matcher _matcher = _pattern.matcher(_string);

        if (_matcher.find()) { //ここで「検索」
            //マッチした場合（"吉田"が含まれている）の処理
            _result = _string.replaceAll("吉田", "よしだ"); 
        } else {
            System.out.println("吉田は含まれていません");
        }
        System.out.println(_string); //=> "吉田松蔭,高杉晋作,久坂玄瑞,吉田稔麿,伊藤博文";
        System.out.println(_result); //=> "よしだ松蔭,高杉晋作,久坂玄瑞,よしだ稔麿,伊藤博文";
    }
}
```

### マッチした数
```
//Main.java
import java.util.regex.*; //Pattern に必要
public class Main { //public は省略可
    public static void main(String[] args) { //決め打ち(自動的に実行)
        String _string = "cabacbbacbcba";
        Pattern _pattern = Pattern.compile("a",Pattern.CASE_INSENSITIVE);
        Matcher _matcher = _pattern.matcher(_string);
        int _count = 0;
        while(_matcher.find()){
            _count++;
        }
        System.out.println(_count); //=> 4
    }
}
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月19日  
更新日：2017年04月12日


<a name="インターフェース（protocol）"></a>
# <b>インターフェース（protocol）</b>

### 概要
* 多くの言語で定義できる interface と同じような機能（protocol と呼ぶ）
* クラスにどのような機能（メソッド）を持たせるかということだけを定める（実際の処理は記述不可）
* カンマ（,）を使って多重実装（複数のプロトコルを同時に指定）が可能

### 例文
```
//test.swift
protocol IMoneybox { //≒interface ←他の言語に合わあせてI○○と命名
    func add(money _money: Int) -> Void
    var total: Int { get set }
}

class Moneybox : IMoneybox { //プロトコルの実装
    private var _total: Int = 0
    func add(money _money: Int) -> Void {
        _total += _money
    } 
    var total: Int {
        get {
            return _total
        }
        set {
            _total = newValue
        }
    }
}

var _tmoneybox: Moneybox = Moneybox()
_tmoneybox.add(money:5000)
print(_tmoneybox.total) //=> 5000
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月29日  
更新日：2017年04月14日


<a name="抽象クラス"></a>
# <b>抽象クラス</b>
* abstract キーワードが存在しない（継承と例外処理等を使って擬似的な抽象クラスを実現する）

```
//test.swift
//==============================================
// 擬似抽象クラスの定義
//==============================================
internal class AbstractClass { //internalは省略可
    //↓共通のメソッド
    internal func common() -> Void { 
        print("AbstractClass.common()")
    }
    //↓抽象メソッドの宣言（実際の処理は書かない）
    internal func abstractMethod() -> Void { 
        print("サブクラスでオーバーライドして実装して下さい") //例外処理でもＯＫ
    }
}

//==============================================
// サブクラス ←擬似抽象クラスを継承
//==============================================
internal class SubClass : AbstractClass { //internalは省略可
    //↓オーバーライドして実際の処理を記述
    override internal func abstractMethod() -> Void {
        print("SubClass.abstractMethod()") //実際の処理
    }
}

var _subClass:SubClass = SubClass()
_subClass.common() //=> "AbstractClass.common()"
_subClass.abstractMethod() //=> "SubClass.method()"
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月29日  
更新日：2017年04月14日


<a name="super"></a>
# <b>super</b>

```
//test.swift
//==================================
// スーパークラス
//==================================
internal class SuperClass { //internalは省略可
    //コンストラクタ
    init(arg: String) {
        print("スーパークラスのコンストラクタ：" + arg)
    }
    //メソッド
    internal func methodSuper(argA: String) -> Void { //internalは省略可
        print("ここはエラーなし") //コンストラクタのsuper()はどこでもOK
        print("スーパークラスのメソッド：" + argA)
    }
}

//==================================
// サブクラス
//==================================
internal class SubClass : SuperClass { //internalは省略可
    //コンストラクタ
    init() {
        super.init(arg:"サブクラスからの呼び出し") //スーパークラスのコンストラクタを呼出す
    }
    //メソッド
    internal func methodSub(argB: String) -> Void { //internalは省略可
        print("ここはエラーなし") //メソッド内のsuper()はどこでもOK!
        super.methodSuper(argA:argB) //スーパークラスのメソッドを呼出す
    }
}

var subClass_: SubClass = SubClass() //サブクラスのインスタンスの生成
//=> "スーパークラスのコンストラクタ：サブクラスからの呼び出し"

subClass_.methodSub(argB:"サブクラスからの呼び出し")
//=> "スーパークラスのメソッド：サブクラスからの呼び出し"
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月29日  
更新日：2017年04月14日


<a name="オーバーライド"></a>
# <b>オーバーライド</b>

### 概要
* スーパークラスで定義したメソッドをサブクラスで再定義（上書き）することをオーバーライドと呼ぶ
* スーパークラスのメソッドを呼び出したい場合は、super.メソッド名(引数名:値) と記述する

### 例文
```
//test.swift
//================
// スーパークラス
//================
internal class SuperClass { //internal は省略可
    //↓サブクラスでオーバーライドされる
    internal func myMethod() -> Void { //internal は省略可
        print("スーパークラスのmyMethod()")
    }
}

//================================
// サブクラス（SuperClassを継承）
//================================
internal class SubClass : SuperClass { //internal は省略可
    //↓スーパークラスのメソッドをオーバーライドする
    override internal func myMethod() -> Void { //internal は省略可
        print("サブクラスのmyMethod()")
        super.myMethod() //スーパークラスのmyMethod()を呼出す場合…
    }
}

//======
// 実行
//======
var subClass_:SubClass = SubClass()
subClass_.myMethod()
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年07月29日  
更新日：2017年04月14日


<a name="カスタムイベント"></a>
# <b>カスタムイベント</b>

### 注意
* addEventListener() の引数（無名関数）のデータ型の前に <b>@escaping</b> が必要

### 例文
```
//test.swift（internalは省略可）
internal class Robot {
    private var _energy: Int = 80

    //無名関数を格納する変数（初期値として何もしない無名関数を定義しておく）
    private var _dieHandler = { (arg:Robot) -> Void in 
        //何もしない
    }

    //引数（無名関数）のデータ型の前に「@escaping」と記述する
    internal func addEventListener(_event:String, _function: @escaping (Robot) -> ()) {
        if (_event == "die") {
            _dieHandler = _function //無名関数を格納する（空の初期値から変更）
        } else { //該当のイベントが無い場合、実行時にerrorを出す（オプション）
            print("error:" + _event + "というイベントはありません") //本来はthrow...を使用
        }
    }

    internal func fight() -> Void {
        _energy -= 20
        if (_energy <= 0) {
           _dieHandler(self) //無名関数の呼び出し
        }
    }
}

//無名関数（リスナー関数）
var die_robot = { (arg: Robot) -> Void in
    print(arg) //=> test.Robot
    print("GAME OVER")
}
print(type(of: die_robot)) //=> (Robot) -> () ←無名関数のデータ型

var _robot: Robot = Robot()
_robot.addEventListener(_event: "die", _function: die_robot) //イベントリスナーの定義
_robot.fight()
_robot.fight()
_robot.fight()
_robot.fight() //=> "GAME OVER"
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年08月01日  
更新日：2017年04月14日


<a name="数学関数"></a>
# <b>数学関数</b>
* インポートするライブラリが OS、関数の種類によって異なるので注意

### sin() : サイン（正弦）
```
//test.swift
import Foundation
print(sin(0.0)) //=> 0.0 ←0°（引数がInt型だとerror）
print(sin(Double.pi/2)) //=> 1.0 ←90°
print(sin(Double.pi)) //=> 1.22464679914735e-16（≒0）←180°
print(sin(Double.pi*3/2)) //=> -1.0 ←270°
print(sin(Double.pi*2)) //=> -2.44929359829471e-16（≒0）
```

### cos() : コサイン（余弦）
```
//test.swift
import Foundation
print(cos(0.0)) //=> 1.0 ←0°（cos(0)だとerror）
print(cos(Double.pi/2)) //=> 6.12323399573677e-17（≒0）←90°
print(cos(Double.pi)) //=> -1.0 ←180°
print(cos(Double.pi*3/2)) //=> -1.83697019872103e-16（≒0）←270°
print(cos(Double.pi*2)) //=> 1.0 ←360°
```

### atan2() : アークタンジェント2
* 2つの値のアークタンジェント（逆タンジェント）
* X、Y 座標の角度をラジアン単位で返す
* Π ラジアン（3.141592…）は180°
```
//test.swift
//三角形の各辺が1:2:√3の場合、2:√3の間の角度は30°であることを検証
import Foundation
var _disX:Double = sqrt(3) //√3のこと
var _disY:Double = 1.0 //※Intは不可
print(atan2(_disY, _disX)) //=> 0.523598775598299（ラジアン）
print(180*atan2(_disY, _disX)/Double.pi) //=> 30.0（度）
```

### M_PI : 円周率
```
//test.swift
import Foundation
print(Double.pi) //=> 3.14159265358979（Double.piラジアン=180°）
```

### floor() : 切り捨て
```
//test.swift
import Foundation
print(floor(1.001)) //=> 1.0
print(floor(1.999)) //=> 1.0
```

### ceil() : 切り上げ
```
//test.swift
import Foundation
print(ceil(1.001)) //=> 2.0
print(ceil(1.999)) //=> 2.0
```

### round() : 四捨五入
```
//test.swift
import Foundation
print(round(1.499)) //=> 1.0
print(round(1.500)) //=> 2.0
```

### abs() : 絶対値
```
//test.swift
import Foundation
print(abs(100)) //=> 100
print(abs(-100)) //=> 100
```

### pow() : 累乗（○の□乗）
```
//test.swift
import Darwin
print(pow(2.0, 0)) //=> 1.0（2の0乗） ←第1引数はIntだとerror
print(pow(2.0, 8)) //=> 256.0（2の8乗） ←第1引数はIntだとerror
```

### sqrt() : 平方根（√○）
```
//test.swift
import Darwin
print(sqrt(2.0)) //=> 1.4142135623731（一夜一夜にひとみごろ）
print(sqrt(3.0)) //=> 1.73205080756888（人並みに奢れや）
print(sqrt(4.0)) //=> 2.0
print(sqrt(5.0)) //=> 2.23606797749979（富士山麓オウム鳴く）
```

### max() : 比較（最大値）
```
//test.swift
import Darwin
print(max(5.01, -10)) //=> 5.01 ←「2つ」の数値の比較
```

### min() : 比較（最小値）
```
//test.swift
import Darwin
print(min(5.01, -10)) //=> -10.0 ←「2つ」の数値の比較
```

実行環境：macOS 10.12.4、Swift 3.1  
作成者：夢寐郎  
作成日：2016年08月01日  
更新日：2017年04月14日
