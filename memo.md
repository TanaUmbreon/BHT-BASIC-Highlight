# メモ

Visual Studio Code でシンタックス ハイライトの拡張機能を自作するうえで引っかかった点などをメモとしてここに記録。

## 導入方法

以下のサイトを参考にして、 VS Code でデバッグしながら作成できる環境を構築。

* [Visual Studio Code でカスタム構文強調エクステンションを作る](https://yogsite.herokuapp.com/programmings/1): ひな形作成に必要なソフトのインストール手順など

## ハイライト構文の記述方法

### 基本形

* `"patterns" : []`: メンバーの値に、マッチング パターンを配列で記述する。
* `"match" : "パターン (正規表現)"`: キーワードなど、ハイライトさせたい単語や要素に一致する正規表現を記述する。
* `"name" : "名前"`: `match` メンバーで指定したパターンに一致した部分に割り当てる名前。キーワード、コメント、文字列、変数、メタ情報など、細かく指定できる。名前には記述ルールがあり、公式ドキュメントのページ末尾に詳細が記載されている。この名前によって、ハイライトの色分けが変わってくる。

#### 例

```json
"patterns": [
    {
        "match": "\\b(?i:DIM|PRIVATE|PUBLIC)\\b",
        "name": "keyword.bhtbasic",
        "comment": "ステートメント (キーワード) として認識される"
    },
    {
        "match": "\\b(?i:CALL|GOSUB|RETURN|END(?!\\s+(FUNCTION|IF|SELECT|SUB)))\\b",
        "name": "keyword.control.bhtbasic",
        "comment": "フロー制御系のステートメント (キーワード) として認識される"
    }
]
```

* `END(?!\\s+(FUNCTION|IF|SELECT|SUB))` は、プログラム終了を命令する `END` ステートメントが、 `END IF` などのコード ブロック終了を表すステートメントの一部分と間違って認識しないようにしている。 `END` の一単語だけならフロー制御のステートメントとして認識するが、 `END IF` など、コード ブロック終了だと認識しなくなる。

### ブロック構造のコード

メソッドや IF 文など、ブロック構成を持ったコードをブロックとして認識させたい場合。

* 作成中

### 参考サイト
* [Visual Studio CodeやAtomのシンタックスハイライト拡張機能を作る](http://qiita.com/Maxfield_Walker/items/51af2984b7a628c41a94): ハイライト構文の書き方を解説
* [TextMate Manual » Language Grammars](https://manual.macromates.com/en/language_grammars): ハイライト構文の公式ドキュメント (英語)

