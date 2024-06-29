# 参照型
processingの型は大きく分けて上の二種類に分けられる。この章では各型の特徴について学ぶ。

## 目次
[参照型の特徴](#参照型の特徴)  
[関数での利用](#関数での利用)  
[参照型での比較](#参照型での比較)  
[演習問題](#演習問題1)

## 参照型の特徴
クラスなどの型はすべて参照型である。c言語をやったことがある場合、構造体のポインタを思い浮かべるとわかりやすいだろう。  
以下のコードを例に示す。
```
class Sample{
  Sample (int n){
    val=n;
  }
  
  int val;
}

void setup(){
  Sample a=new Sample (5);
  Sample b=a;
  b.val=1;
  println (a.val);
}
```
実行結果
```
1

```
上の例で、変数`b`を変更したにもかかわらず`a`の値も変わってしまっている。これは変数に入っている値がインスタンスではなく、インスタンスの場所を示す値であるためである。  
このように変数がインスタンスを参照しているため、このような型を**参照型**と呼ぶ。  
つまり`b=a`によって`a`と`b`が同じインスタンスを参照していることになるため、`b`を書き換えることで`a`も書き換わってしまうのである。  
newを使い、新たにインスタンスを生成するのはこのような事態を避けるためだ。

## 関数での利用
変数に入っている値がインスタンスではなく、インスタンスの場所を示す値であることを利用して関数の引数に渡すとインスタンスの中身を書き換える関数を作成できる。

例. 受け取ったint型の配列を`0`で初期化する関数を利用する
```
void setup(){
  int[] test=new int[10];
  init (test);
  for (int i:test){
    println (i);
  }
}

void init(int[] array){//初期化
    for(int i=0;i<array.length;i++){
        array[i]=0;
    }
}
```

## 参照型での比較
参照型同士で比較をするときは注意が必要である。先の説明の通り参照型の変数が保持する値はインスタンスの場所である。そのため、インスタンスに同じ値が入っていたとしても場所が違うため同じ値か比較することができない。

例. キーボードからの文字列がhelloならworldを返したいが正しく機能しない例
```
void draw(){
}

StringBuilder br;

void keyTyped(){
  br.append(key);
  if (br.toString()=="hello"){//String型は参照型
    println ("world");
  }
}
```

Stringクラスなどの値を管理するような一部のクラスでは、インスタンスが等しいといえるかを調べる場合はequalsメソッドを使うことができる。

例. 上記の例を正しく書き直したもの
```
void draw(){
}

StringBuilder br=new StringBuilder();

void keyTyped(){
  br.append(key);
  if (br.toString().equals("hello")){//equals関数の使用
    println ("world");
  }
}
```
ただし、自身で作成したクラスの場合equals関数を自分で宣言し、実装しておく必要があるため注意が必要である。

## 演習問題[^1]
問1. 以下のクラスに自身のインスタンスを複製し返り値として返すメソッドcloneを追加せよ。
```
class Sample{
  int id;
  float size;

  Sample (int id,float size){
    this.id=id;
    this.size=size;
  }
}
```

[^1]: 演習問題の解答例は[こちら](answers.md)