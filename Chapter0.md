# そもそもprocessingって?
この章ではprocessingを扱う感覚をつかんでもらう。特に理解せずとも、こんなことができるんだ程度に思ってもらって結構。

## 目次
* [環境を整える](#環境を整える)  
* [早速試してみよう](#早速試してみよう)  
* [日本語が文字化けする](#日本語が文字化けする)
* [まとめ](#まとめ)

## 環境を整える
まず最初にprocessingを[processingダウンロードページ](https://processing.org/download)からダウンロードしよう。  
ダウンロードされたファイルを解凍すれば準備完了だ。

## 日本語が文字化けする
画面中央のエディターに日本語を入力すると文字化けすることがある[^1]。この場合ウィンドウ左上の`ファイル>設定`から「エディタとコンソールのフォント」を選び日本語対応しているフォントを選ぶとよい。

## 早速試してみよう
解凍したファイルの中のprocessing.exeを起動すると、エディタが起動する。  
では早速以下のサンプルコードを実行してみよう。入力が終わったら左上の三角ボタンで実行しよう。**escキーで実行を終了できる。**

```java
void setup (){
  size (1000,1000);
  noStroke ();
  reset();
}

void reset (){
  box=new Box ();
}

class Box{
  float rad;
  int speed=1;
  float x,y,dx,dy;
  
  Box (){
    x=y=0;
    dx=dy=100;
    rad=random (PI/2);
  }
  
  void move (){
    x+=cos(rad)*speed;
    y+=sin(rad)*speed;
    if (y<0||y+dy>height){
      rad*=-1;
    }
    if (x<0||x+dx>width){
      rad=PI-rad;
    }
    if (rad>2*PI){
      rad-=2*PI;
    }
    if (rad<0){
      rad+=2*PI;
    }
  }
  
  void draw (){
    fill (255);
    rect (x,y,dx,dy);
    textAlign (CENTER,TOP);
    fill (0);
    textSize (60);
    text ("DVD",x+dx/2,y);
    ellipse (x+dx/2,y+dy/2+dy/4,dx,dy/2);
    fill (255);
    ellipse (x+dx/2,y+dy/2+dy/4,dx/4,dy/8);
  }
}

Box box;

void draw (){
  background (255);
  box.move ();
  fill (255);
  box.draw ();
}
```
 
上手く実行できただろうか。

## まとめ

processingは比較的少ないコードの量でゲームを手軽に作れるので興味があるならぜひ挑戦してほしい。  
ほかの言語には劣るものの、比較的知名度も高いため調べれば実装方法などは出てくる。  
しかし、基礎ができているとその実装に対する理解を高めることができるため、ぜひこのテキスト(他に参考書を持っていてそちらの方がいいという人はそれでも良し)を読み進めていただきたい。

[^1]: というかデフォルトの設定だと、十中八九文字化けする。