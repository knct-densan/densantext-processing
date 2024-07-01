# クラスの継承
似たような役割を持ったクラスを作りたくなったことはないだろうか。そんな時に使えるものが継承である。

## 目次
[継承](#継承)
[親クラスの要素を明示的に呼び出す](#親クラスの要素を明示的に呼び出す)
[オーバーライド](#オーバーライド)
[継承を禁止する](#継承を禁止する)
[演習問題](#演習問題1)

## 継承
継承とはすでにあるクラスをもとに、新しいフィールドやメソッドを追加したり、上書きすることのできる仕組みである。

例えば、文字が表示されるボタンと画像が表示されるボタンの二種類のクラスを作りたいとする。こういったとき、ボタンの仕組みをそれぞれのクラスに作るのは手間がかかる。また、ボタンの仕様変更の際にも両方のクラスに手を加えなくてはならない。それにより思わぬバグが混入する恐れもある。  
ではどうするかというと、ボタンの仕組みのクラスを一つ作ってからそのクラスを継承すればいいのだ。

継承するには以下のように記述する。
```
class クラス名 extends 継承するクラス名{
  ここにフィールドやメソッドを記述
}
```
継承するクラス名を親クラス(スーパークラス)、継承したクラスを子クラス(サブクラス)と呼ぶ。また、processingは多重継承を認めていないため、一度に継承できるクラスは一つだけである。  
また、子クラスのコンストラクタが実行される前に自動的に親クラスのコンストラクタが呼び出される。

例. 親クラス
```
class Super{
  String str;
  
  Super (){
    str="親クラス";
    println ("親のコンストラクタ");
  }
  
  void putNum (int n){
    println (str+n);
  }
}
```
例. 子クラス
```
class Sub extends Super{
  Sub (){
    str="子クラス";//親クラスのフィールドが使える
  }
  
  void putNum (){
    putNum (100);//親クラスのメソッドが使える
  }
}
```

## 親クラスの要素を明示的に呼び出す
`super.フィールド名`または`super.メソッド名(引数)`と記述すると、親クラスの要素を明示的に呼ぶことができる。そのため、以下の例のように子クラスでフィールドを上書きしても呼び出すことが可能になる。  
また、親クラスのコンストラクタは`super (引数)`と書くことで呼び出せる。コンストラクタの呼び出しは親クラスのものでも、自身のコンストラクタの一行目にしか記述ができない。

例. 親クラス
```
class Super{
  int a;
  
  Super (int n){
    a=n;
  }
  
  void putVal (){
    println (a);
  }
}
```
例. 子クラス
```
class Sub extends Super{
  int a;//フィールドの上書き
  
  Sub (int n1,int n2){
    super (n1);//親クラスのコンストラクタ
    b=n2;
  }
  
  void putVal2 (){
    println (a);
  }
  
  void putSum (){
    println (a+super.a);
  }
}
```

## オーバーライド
子クラスに親クラスのメソッドと全く同じ返り値の型、名前、引数をとるメソッドを作成する場合を特別にオーバーライドと呼ぶ。オーバーライドする関数の前に`@Override`と記述すると明示的にオーバーライドできる。記述されている場合、実行時にオーバーライド可能かを確かめ、オーバーライドできない場合はエラーを出力する。

例. 親クラスにするButtonクラス
```
class Button{
  float x,y,dx,dy;
  
  void draw (float x,float y,float dx,float dy){
    fill (255,0);//判定可視化用
    rect (x,y,dx,dy);
    this.x=x;
    this.y=y;
    this.dx=dx;
    this.dy=dy;
  }
  
  boolean checkHover (){
    if (mouseX>x&&mouseX<x+dx&&mouseY>y&&mouseY<y+dy){
      return true;
    }
    return false;
  }
}
```
例. 子クラスのImageButtonクラス
```
class ImageButton extends Button{
  PImage img;
  
  ImageButton (PImage img){
    this.img=img;
  }

  void draw (float x,float y){
    draw (x,y,img.width,img.height);
  }
  
  void draw (float x,float y,float dx){
    draw (x,y,dx,img.height*dx/img.width);
  }
  
  @Override
  void draw (float x,float y,float dx,float dy){//オーバーライド
    super.draw (x,y,dx,dy);
    image (img,x,y,dx,dy);
  }
}
```

## 継承を禁止する
クラスの中には継承を禁止しているクラス(Stringなど)が存在している。禁止の仕方は簡単でクラスの宣言前に、`final`を付け加えるだけである。
```
final class Sample{
}

class Test extends Sample{//継承できない
}
```

## 演習問題[^1]
問1. ArrayList&lt;String&gt;を継承したStrListクラスを作成し、putallメソッドを追加せよ。putAllメソッドは実行されるとリスト内の全要素を出力する。


[^1]: 演習問題の解答例は[ここ](answers.md)
