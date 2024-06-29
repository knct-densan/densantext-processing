# クラスを自作する
processing標準のクラスではゲームのパーツとしては力不足かもしれない。そこで、自分でクラスを作ることで力不足を解消できる。この章ではクラスの宣言方法を学ぶ。

## 目次
[新しいタブを開く](#新しいタブを開く)  
[クラスの宣言](#クラスの宣言)  
[フィールドとメソッドの引数の名前が被ったとき](#フィールドとメソッドの引数の名前が被ったとき)  
[コンストラクタ](#コンストラクタ)  
[コンストラクタからコンストラクタを呼び出す](#コンストラクタからコンストラクタを呼び出す)  
[演習問題1](#演習問題1)

## 新しいタブを開く
クラスの宣言は多くの場合長くなりがちであるため新しいタブに記述することを推奨する。新しいタブを開く場合、スケッチ名の右側のボタンから新規タブを選択する。

## クラスの宣言
クラスは以下のようにすることで簡単に宣言できる。クラス名は通例で一文字目を大文字で書く。
```
class クラス名{
  ここにフィールドやメソッドを記述
}
```

例. `(x,y)`を中心に半径`r`、周期`T`で回転する、直径`pd`の点のクラス
```
class RotatePoint{
  int x,y,r,T,pd;
  float rad;
  
  void rotate (){
    rad+=2*PI/(T*60);
  }
  
  void draw (){
    fill (0);
    circle (x+r*cos(rad),y+r*sin(rad),pd);
  }
}
```
例. RotatePointクラスの使用例
```
void setup (){
  size (500,500);
  p=new RotatePoint ();
  p.pd=3;
  p.r=200;
  p.x=p.y=250;
  p.T=10;
  p.rad=0;
}

RotatePoint p;

void draw (){
  background (255);
  p.draw();
  p.rotate();
}
```

## フィールドとメソッドの引数の名前が被ったとき
フィールドとメソッドの引数の名前が被ると、引数が優先されてしまい正しく動作しない。対処として、`this`を使用するという方法がある。  
`this`は自分自身のインスタンスという意味で、`this.フィールド名`で確実にフィールドを呼び出すことができる。

## コンストラクタ
インスタンスが生成されたときに実行されるメソッドを特別にコンストラクタと呼ぶ。返り値が設定できず、名前もクラスと同じにしなければならない。  
インスタンスの生成の時に渡す引数はこのコンストラクタの引数として渡される。  
主にフィールドの初期化に使用される。

以下のように書く。
```
class TestClass{
  TestClass (){
    処理
  }
}
```
例. RotatePointクラスとその使用例の書き換え
```
class RotatePoint{
  int x,y,r,T,pd;
  float rad;
  
  RotatePoint (int x,int y,int r,int T,int pd){
    rad=0;
    this.x=x;
    this.y=y;
    this.r=r;
    this.T=T;
    this.pd=pd;
  }
  
  void rotate (){
    rad+=2*PI/(T*60);
  }
  
  void draw (){
    fill (0);
    circle (x+r*cos(rad),y+r*sin(rad),pd);
  }
}
```
```
void setup (){
  size (500,500);
  p=new RotatePoint (250,250,200,10,3);
}

RotatePoint p;

void draw (){
  background (255);
  p.draw();
  p.rotate();
}
```

また、コンストラクタもオーバーロード可能であるためインスタンスの生成時の引数によって場合分けが可能である。また、コンストラクタはインスタンスの生成時のみにしか実行できないため、それ以外のところで呼び出そうとするとエラーを返される。

## コンストラクタからコンストラクタを呼び出す
別のコンストラクタはコンストラクタの一行目であれば、`this(引数)`呼び出すことができる。これを利用して引数がなかった時の初期値の設定を簡単にできる。

例. RotatePointで引数無しのコンストラクタを記述
```
class RotatePoint{
  int x,y,r,T,pd;
  float rad;

  RotatePoint (){
    this (0,0,0,0,0);//別のコンストラクタの呼び出し
  }
  
  RotatePoint (int x,int y,int r,int T,int pd){
    rad=0;
    this.x=x;
    this.y=y;
    this.r=r;
    this.T=T;
    this.pd=pd;
  }
  
  void rotate (){
    rad+=2*PI/(T*60);
  }
  
  void draw (){
    fill (0);
    circle (x+r*cos(rad),y+r*sin(rad),pd);
  }
}
```

## 演習問題[^1]
問1. 学年、組、出席番号を表すint型の変数`grade`、`group`、`number`と名前を表すString型の変数`name`を持つStudentクラス**のみ**を作成せよ。  
また、このクラスが持つメソッドは`void getIngo()`のみであり、このメソッドはコンソールに`[学年]年[組]組[出席番号]番:[名前]`のように出力するものである。  
なお、各変数はコンストラクタ`Student ([学年],[組],[出席番号],[名前])`により初期化できるようにしておくこと。

初期化例
```
Student student=new Student (1,2,15,"試験的生徒");
```
出力例
```
1年2組15番:試験的生徒

```

[^1]: 演習問題の解答例は[こちら](answers.md)