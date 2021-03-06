### <b>この項目は編集中です</b>

# SQLite with Python（ Windows ）

## <ruby>SQLite<rt>エスキューライト</rt></ruby> について

* 2000年に登場したオープンソースの軽量コンパクトな [RDBMS](http://bit.ly/2lunAUm)。
* 大規模なシステムには不向きだが、中小規模のデータを扱う限りでは高速に処理（同時書き込みが不可）。
* ファイル単位で処理されるためバックアップが容易。
* データベースユーザーの概念が無いため、パスワードの設定は不可。
* [.htacess](http://www.weblio.jp/content/Htaccess) を使い .sqlite3 ファイルに対してアクセス制限を設定しないとファイル（xxx.sqlite3）を直接ダウンロード出来てしまう。
* データの操作を行う[問い合わせ言語](http://bit.ly/2mvUUPR)として [SQL](https://ja.wikipedia.org/wiki/SQL) を利用。

## 開発環境の構築

|カテゴリ|ソフトウェア|リリース|
|:--:|:--:|:--:|
|OS|[Windows](https://ja.wikipedia.org/wiki/Microsoft_Windows) 10（64bit）|ー|
|ソフトウェア|[XAMPP](https://ja.wikipedia.org/wiki/XAMPP) 8.0.6|2021年5月|
|Web サーバ|Apache 2.4.47|2020年04月|
|データベース|[SQLite](https://ja.wikipedia.org/wiki/SQLite) 3.33.0|2020年08月|
|実行エンジン|PHP 8.0.6|2021年05月|
|エディタ|Visual Studio Code 1.56.2|2021年05月|
|拡張機能|PHP Debug 1.15.1|ー|
|拡張機能|[vscode-database](http://bit.ly/2mh8nYF) 2.2.3|ー|
|ブラウザ|Google Chrome 91.0|2021年05月|

1. [XAMPP](https://ja.wikipedia.org/wiki/XAMPP) のインストール
    1. https://www.apachefriends.org/download.html にアクセス
    1. [XAMPP for Windows 7.3.28, 7.4.19 & 8.0.6] の [8.0.6 / PHP 8.0.6] の [Download（64bit）] をクリック、ダウンロード
    1. ダウンロードした .exe ファイルをダブルクリック、インストール
    1. XAMPP Control Panel が起動したら Service（<b>Apache</b>） の [Start] ボタンをクリック

1. Web サーバのドキュメントルート（ C:\xampp\htdocs ）に以下の内容の test.php ファイルを置き、Webブラウザで localhost/test.php を開いて各種情報を確認（<b>本番環境ではセキュリティ上削除しておく</b>）
    ```
    <?php phpinfo(); ?>
    ```

1. バージョン確認（以下の test.php を Web サーバ上で実行）  
    ※ドキュメントルートは（ C:\xampp\htdocs ）
    ```
    <?php
        $con = new PDO('sqlite::memory:', null, null);
        $statement = $con->prepare('SELECT sqlite_version()');
        $statement->execute();
        echo $statement->fetchColumn(); //=> 3.33.0
    ?>
    ```

1. エディタで C:\xampp\php\php.ini を開いて、エラー表示が有効か確認する（<b>本番環境では Off にする</b>）
    ```
    501行目 display_errors=On  
    ```

1. Visual Studio Codeに拡張機能の追加  
    [表示] → [拡張機能] から PHP Debug と [vscode-database](http://bit.ly/2mh8nYF) を検索＆インストール


1. コードの記述（test.php）
```
<?php
    // データベースの作成（既存の場合はファイルを開く）
    $con = new PDO("sqlite:test.sqlite3"); //慣例的に xxx.sqlite3 とする

    // テーブルの作成（xxx_tb が無い場合のみ作成）
    $sql = "CREATE TABLE IF NOT EXISTS hello_tb(country TEXT, words TEXT)";
    $statement = $con->prepare($sql); //prepare() メソッド
    $statement->execute();

    //データの挿入（今回のサンプルでは実行する度に追加される）
    $sql = "INSERT INTO hello_tb VALUES('english', 'Hello,world!')";
    $statement = $con->prepare($sql);
    $statement->execute();

    //データの抽出
    $sql = "SELECT * FROM hello_tb WHERE country='english'";
    $statement = $con->prepare($sql);
    $statement->execute();
    foreach ($statement as $theRecord) {
        echo $theRecord["words"]."<br>";
    }
?>
```

## 実行

1. Web ブラウザ（Google Chrome）を起動

1. [localhost](https://ja.wikipedia.org/wiki/Localhost)/test.php を開く

1. Hello,world! と表示されたら成功！

***
作成者: 夢寐郎  
作成日: 2017年07月26日  
更新日: 2021年05月29日