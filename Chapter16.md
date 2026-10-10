# JSONを使ってみよう
テキストデータに比べると複雑だが、取り回しの良いデータ構造であるJSONを扱ってみよう。

## 目次
* [JSONとは](#jsonとは)
    * [オブジェクト型](#オブジェクト型)
    * [文字列型](#文字列型)
    * [数値型](#数値型)
    * [真偽値型](#真偽値型)
    * [配列型](#配列型)
    * [null](#null)
* [processingでJSONを扱ってみよう](#processingでJSONを扱ってみよう)
    * [オブジェクト型からデータを取り出すとき](#オブジェクト型からデータを取り出すとき)
    * [配列型からデータを取り出すとき](#配列型からデータを取り出すとき)
* [演習問題](#演習問題1)

## JSONとは
JSONとはjavascriptのオブジェクト記述をもとにしたデータ構造である。  
以下に基本的な構造を示す。
```json
{
    "キー": "値"
}
```
見ての通りJSONはキーと値が紐づいているため、データの構造を変更しても実際にプログラム上で手を加えるのは変更した部分に関するところだけでよいため非常に楽である。

JSONは様々なデータ型が存在しており、それぞれを値に使用することができる。  
基本的なデータ型は以下の通りである。
* オブジェクト型
* 文字列型
* 数値型
* 真偽値型
* 配列型
* null

### オブジェクト型
Object型はJSONにおいて基本の型である。波かっこで囲まれた構造になっており、中にはキーと値を組み合わせた情報が格納されている。

例. Object型の記述例
```json
{
    "key": "value"
}
```
カンマで区切ってキーを複数持たせたり、値にObject型を指定して入れ子構造にすることもできる。

例. 複雑なObject型の例
```json
{
    "type": "player",
    "status": {
        "hp": 10,
        "pow": 1,
        "def": 200
    }
}
```

### 文字列型
文字列型はダブルクォーテーションで囲まれた値である。バックスラッシュで`\n`などのエスケープ文字が使用できる。

例. 文字列型の例
```json
{
    "washini_shine": "ふむ...... %s というんだな!"
}
```

### 数値型
整数でも小数でも扱うことができる。processingで扱う際は小数のデータを整数として取り出さないように注意すること。
また、指数を表すときは`e`(大文字か小文字かは問わない)のあとに記述することで表現できる。

例. 数値型の例
```json
{
    "AVOGADRO": 6.02214076e-23
}
```

### 真偽値型
`true`か`false`のどちらかの値のみを受け付ける。

例. 真偽値型の例
```json
{
    "finish_game": false
}
```

### 配列型
好きな値をカンマ区切りで並べることのできる型。一つのキーに複数の値を紐づけたい時に便利。

例. 配列型の例 (何のデータかあててみてね minecraft ver.26.1時点)
```json
{
  "values": [
    "minecraft:carrot",
    "minecraft:potato",
    "minecraft:beetroot"
  ]
}
```

### null
データがないことを表す。

例. nullの使用例
```json
{
    "???PointerException <- ???に入る文字は?": null
}
```

## processingでJSONを扱ってみよう
### オブジェクト型からデータを取り出すとき
まず、初めに以下のJSONをスケッチフォルダ直下の`data`フォルダ内に配置してほしい。

**data.json**
```json
{
    "title":"JSON解説",
    "info":{
        "club": "densan club",
        "lang": "processing"
    },
    "data":[
        {
            "float": true,
            "value": 1.5
        },
        {
            "float": false,
            "value": 2
        },
        {
            "float": false,
            "value": 3
        },
        {
            "float": true,
            "value": 2.5
        },
        {
            "float": false,
            "value": 4
        }
    ]
}
```

ファイルからJSONを読む際は`loadJSONObject`関数を使用する。  
実際に先ほど作成した`data.json`を読み込んでみよう。

```java
void setup(){
    //読み込んだ情報はJSONObjectクラスの変数になるぞ!
    JSONObject json=loadJSONObject("data.json");//data.jsonを読み込む
}
```

では、試しに読んだデータから`title`キーに紐づいている情報を取得してみよう。
データを取得する際は`JSONObject`クラスのメソッドを利用する。

* `JSONObject.getJSONObject(<キー: String>)`: オブジェクト型のデータを取得する
* `JSONObject.getString(<キー: String>)`: 文字列型のデータを取得する
* `JSONObject.getInt(<キー: String>)`: 数値型(整数)のデータを取得する
* `JSONObject.getFloat(<キー: String>)`: 数値型(小数)のデータを取得する
* `JSONObject.getBoolean(<キー: String>)`: 真偽値型のデータを取得する
* `JSONObject.getJSONArray(<キー: String>)`: 配列型のデータを取得する

`title`キーに紐づいている情報は文字列であるため、`getString`メソッドを使用しよう。

```java
void setup(){
    //読み込んだ情報はJSONObjectクラスの変数になるぞ!
    JSONObject json=loadJSONObject("data.json");//data.jsonを読み込む

    String title=json.getString("title");//titleキーの情報の取得
    println(title);//取得した情報の出力
}
```

次は`info`内の`club`に紐づいている情報を取得してみよう。
今回の構造はオブジェクト型が間に挟まっているが、やることは文字列の時と同じで、丁寧に情報を取得すれば難しくはない。

```java
void setup(){
    //読み込んだ情報はJSONObjectクラスの変数になるぞ!
    JSONObject json=loadJSONObject("data.json");//data.jsonを読み込む

    JSONObject info=json.getJSONObject("info");//infoキーの情報の取得
    String club=info.getString("club");//clubキーの情報の取得
    println(club);//取得した情報の出力
}
```
面倒であれば次のように書いても問題はないだろう。
```java
void setup(){
    //読み込んだ情報はJSONObjectクラスの変数になるぞ!
    JSONObject json=loadJSONObject("data.json");//data.jsonを読み込む

    String club=json.getJSONObject("info").getString("club");//一気にclubキーの情報の取得までする
    println(club);//取得した情報の出力
}
```
### 配列型からデータを取り出すとき
配列型からデータを取り出すときは、オブジェクト型から取り出す時と違ってキーの代わりにインデックス番号を指定する必要がある。
試しに`data`キーの二つ目の要素(インデックス番号は1)を取り出して出力してみよう。

```java
void setup(){
    //読み込んだ情報はJSONObjectクラスの変数になるぞ!
    JSONObject json=loadJSONObject("data.json");//data.jsonを読み込む

    JSONArray data=json.getJSONArray("data");//dataキーの情報の取得
    JSONObject second_data=data.getJSONObject(1);//二つ目の情報の取得
    println(second_data);//取得した情報の出力
}
```
なお、配列の要素数は`size`メソッドで取得することができる。

## 演習問題[^1]
問1. `data.json`の`value`キーの値を`float`キーの値に応じて出力を分けよ。
出力例. 
```
小数: 1.5
整数: 2
整数: 3
小数: 2.5
整数: 4
```

[^1]: 演習問題の解答例は[ここ](answers.md)