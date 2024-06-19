# クラスとインスタンス
この章ではクラスについての詳しい説明をしていく。

## 目次
[クラスとは](#クラスとは)  
[用意されているクラスを使う](#用意されているクラスを使う)  
[演習問題](#演習問題1)

## クラスとは
クラスとは様々な要素を集めて一つの新しい型として扱うための機能である。  
クラスの要素には変数だけでなく関数も利用することができ、クラス特有の動作を実現できる。  
また、クラスに含まれる変数をフィールド、関数をメソッドと呼ぶ。

## 用意されているクラスを使う
まずクラスを利用するには、インスタンスと呼ばれる実体が必要である。インスタンスを生成するには以下のように書く。
```
new クラス名(引数)
```
この書き方を見ればわかるが実は[配列](Chapter4.md)もクラスの一つである。  
よってクラスの変数を用意するにはこのように書く。
```
クラス名 変数名=new クラス名(引数);
```
また、フィールドやメソッドにアクセスするには変数の後にピリオドを付ける必要がある。

例. フィールドにアクセス
```
変数名.フィールド名;
```
以下にprocessingでよく使われるクラスの一例をあげる。

### Stringクラス
Stringクラスだけ特別でnewを書くことなく使用することができる。しかしnewを書いて使うこともできる。

例. String型の変数`str`を宣言しnewを使って`"Hello World!"`で初期化
```
String str=new String ("Hello World!");
```

また、Stringクラスのメソッドにはn文字目の文字を取得するcharAtメソッドや、文字が何番目に含まれるかを検索するindexOfメソッドなどが存在する。
```
String str=new String ("Hello World!");

void setup (){
  println (str.charAt(4));//4番目の文字を取得(ただし先頭は0番目)
  println (str.indexOf('W'));//文字が何番目か検索(ただし先頭は0番目)
  println (str.length());//全体の文字数を取得
  println (str.substring(3,10));//3文字目以降で10文字目より前の文字列を切り取る(ただし先頭は0番目)
}
```

### StringBuilderクラス
文字列を編集するときに使うクラスである。文字列の連結、文字の置き換え、文字の削除等のかゆいところに手が届くクラスである。

例. StringBuilderの機能
```
StringBuilder str=new StringBuilder ("Hello World!");

void setup (){
  println (str.charAt(4));//4番目の文字を取得(ただし先頭は0番目)
  println (str.indexOf("W"));//文字が何番目か検索(ただし先頭は0番目)
  println (str.length());//全体の文字数を取得
  println (str.substring(3,10));//3文字目以降で10文字目より前の文字列を切り取る(ただし先頭は0番目)
  println (str.delete(0,6));//0~5文字目を削除
  println (str.insert(0,"Hello "));//先頭に文字を挿入
  println (str.append ("Let's processing!"));//文字列の連結(連結する物は文字列でなくてもよい)
  println (str.toString());//String型に変換
  str.setLength (5);//文字数を5に設定(返り値がない)
  println (str);
}
```

### ArrayListクラス
大きさを自由に変えることのできる配列(可変長配列)のクラス。addメソッドで要素の追加removeメソッドで要素の削除を行える。先頭の要素は0番目。

例. 任意のクラスの可変長配列`array`の宣言
```
ArrayList<クラスの型> array=new ArrayList();
```

例. 追加と削除
```
void setup (){
  ArrayList<String> strs=new ArrayList();
  strs.add ("Hello");//要素の追加
  strs.add ("Goodbye");//要素の追加
  strs.add ("World!");//要素の追加
  strs.add (2,"Java");//要素を二番目に追加
  strs.remove (1);//一番目の要素を削除
  for (String str:strs){
    println (str);
  }
  println ("配列のサイズ : "+strs.size());
  strs.clear ();//要素の全消し
  for (String str:strs){
    println (str);
  }
  println ("配列のサイズ : "+strs.size());
}
```

また、ArrayListでintなどクラスではない型を扱いたいときには[ラッパークラス](#ラッパークラス)と呼ばれるクラスを利用する必要がある。

クラスの型にObject型を使うとなんでも入れることができるようになる。
```
ArrayList<Object> array=new ArrayList();
void setup (){
  array.add (10);//Integer型
  array.add ("test");//String型
  array.add ('c');//Character型
  array.add (true);//Boolean型
  array.add (2.0);//Float型
  for (Object i:array){
    println (i);//各要素の表示
  }
}
```

### ラッパークラス
ラッパークラスとはintなどクラスではない型と対応したクラスである。

例. ラッパークラスの一例
|型|ラッパークラス|
|-|-|
|`int`|`Integer`|
|`char`|`Character`|
|`float`|`Float`|
|`boolean`|`Boolean`|

また、ラッパークラスはクラスであるが元の型と概ね同じような使い方ができ、型の値をラッパークラスに変化させることをボックス化(ボクシング)、ラッパークラスから元の型に戻すことをボックス化解除(アンボクシング)と呼ぶ。

```
void setup (){
  Integer val1=10;//int → Integer (ボックス化)
  int val2=val1;//Integer → int (ボックス化解除)
  val1=val2+5;//int → Integer
  println (val1);
  println (val2);
}
```

## 演習問題[^1]
問1. ArrayListクラスを利用し、キーボードから入力された文字を格納し、改行文字(`'\n'`)の入力で格納した文字を全て出力するプログラムを作成せよ。また、文字を出力した後は配列を空にしておくこと。

問2. 問1のプログラムをStringBuilderを用いて書き換えよ。

[^1]: 演習問題の解答例は[こちら](answers.md)