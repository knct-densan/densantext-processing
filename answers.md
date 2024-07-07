# 演習問題 解答例
各章の演習問題の解答例です。

## 目次
1. [変数と定数と標準出力](#1-変数と定数と標準出力)
2. [変数と計算](#2-変数と計算)
3. [制御文](#3-制御文)
4. [配列](#4-配列)
5. [関数](#5-関数)
6. [変数の有効範囲](#6-変数の有効範囲)
7. [画面の描画がしたい](#7-画面の描画がしたい)
8. [キーボードとマウス](#8-キーボードとマウス)
9. [クラスとインスタンス](#9-クラスとインスタンス)
10. [クラスを自作する](#10-クラスを自作する)
11. [参照型](#11-参照型)
12. [クラスの継承](#12-クラスの継承)
13. [画像を扱う](#13-画像を扱う)

## 1. 変数と定数と標準出力
問1.
```java
void setup (){
  println (PI);
}
```

## 2. 変数と計算
問1.
```java
void setup (){
  println (8/3);
}
```

問2.
```java
void setup (){
  println ((int)'a');
}
```

## 3. 制御文
問1.
```java
void setup (){
  for (int i=0;i<=45;i+=3){
    println (i);
  }
}
```

## 4. 配列
問1.
```java
void setup (){
  int[] array=new int[5];
  for (int i=0;i<array.length;i++){
    array[i]=i;
  }
  for (int i:array){
    println (i);
  }
}
```

## 5. 関数
問1.
```java
int big (int n){
  return n*2;
}
```

問2.
```java
void tri (int hei){
  for (int i=0;i<hei;i++){
    for (int j=0;j<=i;j++){//iが増えるとjの最大値も増える
      print ('*');
    }
    println ();
  }
}
```

## 6. 変数の有効範囲
問1.
```java
void setup(){
  n=0;
}

void put(){
  println (n+10);
}

int n;//グローバル変数
```

## 7. 画面の描画がしたい
問1.
```java
void setup (){
  size (500,500);//サイズ
  background (255);//背景色
}
```
問2.
```java
void setup (){
  fullScreen ();//全画面
}

int i=0;

void draw (){
  background (255);
  fill (255,0,0);//塗りつぶしの色
  rect (width/2-150+i++,height/2-150,300,300);//四角形
}
```

## 8. キーボードとマウス
問1.
```java
void setup (){
  background (255);
}

void draw (){
}

int pressNum=0;

void keyPressed (){
  switch (++pressNum%4){//キーが押されるたびに更新
    case 0:
    background (255);
    break;
    
    case 1:
    background (255,0,0);
    break;
    
    case 2:
    background (0,255,0);
    break;
    
    case 3:
    background (0,0,255);
    break;
  }
}
```

問2.
```java
void setup (){
  size (500,500);
}

void draw (){
  background (255);
  circle (mouseX,mouseY,20);//マウスポインタの位置
}
```

問3.
```java
void setup (){
  size (500,500);
}

void draw (){
  if (mouseX>100&&mouseX<400&&mouseY>100&&mouseY<400){//範囲内かを判定
    background (255,0,0);
  }else{
    background (255);
  }
  fill (0,255,0);
  rect (100,100,300,300);
}
```

## 9. クラスとインスタンス
問1.
```java
ArrayList<Character> buf=new ArrayList();//charの可変長配列

void draw(){
}

void keyTyped (){
  buf.add(key);
  if (key=='\n'){//改行文字であるとき
    for (char c:buf){//配列の全要素を出力する
      print (c);
    }
    buf.clear();
  }
}
```

問2.
```java
StringBuilder buf=new StringBuilder();

void draw(){
}

void keyTyped (){
  buf.append(key);
  if (key=='\n'){
    print (buf);
    buf.setLength(0);//要素をクリア
  }
}
```

## 10. クラスを自作する
問1.
```java
class Student{
  int grade,group,number;
  String name;
  
  Student (int grade,int group,int number,String name){//初期化
    this.grade=grade;
    this.group=group;
    this.number=number;
    this.name=name;
  }
  
  void getInfo (){//出力
    println (grade+"年"+group+"組"+number+"番:"+name);
  }
}
```

## 11. 参照型
問1.
```java
class Sample{
  int id;
  float size;

  Sample (int id,float size){
    this.id=id;
    this.size=size;
  }
  
  Sample clone (){
    return new Sample (id,size);//インスタンスを生成
  }
}
```

## 12. クラスの継承
問1
```java
class StrList extends ArrayList<String>{
  void putAll (){
    for (String str:this){
      println (str);
    }
  }
}
```

## 13. 画像を扱う
問1.
```java
void drawImage (PImage img,float x,float y,float a){
  image (img,x,y,img.width*a,img.height*a);//幅、高さをそれぞれa倍
}
```

## 14. 音声データを使う(Minimライブラリの使用)
問1.
```java
import ddf.minim.*;
import ddf.minim.analysis.*;
import ddf.minim.effects.*;
import ddf.minim.signals.*;
import ddf.minim.spi.*;
import ddf.minim.ugens.*;

Minim minim=new Minim (this);
AudioPlayer player;

void setup (){
  player=minim.loadFile ("ファイルのパス");//必要に応じて変更
  windowDraw ();
}

void draw(){
}

void windowDraw (){//画面の描画
  background (255);
  fill (0);
  textAlign (CENTER,CENTER);
  textSize (50);
  if (player.isPlaying()){
    text ("play",width/2,height/2);
  }else{
    text ("stop",width/2,height/2);
  }
}

void keyPressed (){
  if (key==' '){
    if (player.isPlaying ()){
      player.pause();
    }else{
      player.loop();
    }
  }
  if (keyCode==RIGHT){
    int time=player.position()+10000;
    while (player.length()<=time){//領域外の時
      time-=player.length();
    }
    player.cue (time);
  }
  if (keyCode==LEFT){
    int time=player.position()-10000;
    while (0>time){//領域外の時
      time+=player.length();
    }
    player.cue (time);
  }
  windowDraw ();//画面の更新
}
```
問2.
```java
import ddf.minim.*;
import ddf.minim.analysis.*;
import ddf.minim.effects.*;
import ddf.minim.signals.*;
import ddf.minim.spi.*;
import ddf.minim.ugens.*;

Minim minim=new Minim (this);
PlayBar bar;
AudioPlayer player;

void setup (){
  size (600,600);
  player=minim.loadFile ("ファイルのパス");//必要に応じて変更
  bar=new PlayBar (0,height-5,width,10,20,color(200,0,0),color(255,0,0));//再生バーの初期位置、色
}

void draw (){
  windowDraw ();//毎フレーム画面を更新
}

float playPoint;//再生バーのポイント位置
boolean dragged=false,played=false;

void windowDraw (){//画面の描画
  background (255);
  fill (0);
  textAlign (CENTER,CENTER);
  textSize (50);
  if (player.isPlaying()){
    text ("play",width/2,height/2);
  }else{
    text ("stop",width/2,height/2);
  }
  float tmp=bar.dragPoint();//何割再生されたか
  if (bar.drag){//再生バーのポイントがドラッグされているとき
    player.pause();
    bar.draw();//再生バーの描画
    playPoint=tmp;//再生位置の保存
    dragged=true;
  }else{
    if (dragged){//前のフレームまでドラッグされていた時
      dragged=false;
      player.cue((int)(player.length()*playPoint));//再生位置の更新
      if (played){//ドラッグ前に再生されていた時のみ再生を再開
        player.loop();
      }
    }
    played=player.isPlaying();//再生されているか
    bar.draw(player.position(),player.length());//再生バーの描画
  }
}

void keyPressed (){
  if (key==' '){
    if (player.isPlaying ()){
      player.pause();
    }else{
      player.loop();
    }
  }
  if (keyCode==RIGHT){
    int time=player.position()+10000;
    while (player.length()<=time){
      time-=player.length();
    }
    player.cue (time);
  }
  if (keyCode==LEFT){
    int time=player.position()-10000;
    while (0>time){
      time+=player.length();
    }
    player.cue (time);
  }
}

class PlayBar{//再生バー
  float px,pr;//ポイントのx座標と半径
  float lsx,ly,lfx,lweight;//再生バーのx座標の始点、終点とy座標
  color lineC,pointC;//色情報
  
  PlayBar (float linesx,float liney,float linefx,float lineWeight,float pointr,color line,color point){
    this (linesx,liney,linefx,lineWeight,0,pointr,line,point);
  }
  
  PlayBar (float linesx,float liney,float linefx,float lineWeight,float pointx,float pointr,color line,color point){//初期化
    lsx=linesx;
    ly=liney;
    lfx=linefx;
    px=pointx;
    pr=pointr;
    lweight=lineWeight;
    lineC=line;
    pointC=point;
  }
  
  void draw (){
    draw (px,lfx-lsx);
  }
  
  void draw (float playPoint,float playLength){//再生バーの描画
    push ();//なくてもいい(描画スタイルの保存)
    px=(lfx-lsx)*(playPoint/playLength);//ポイントの位置
    stroke (200,200,200);//バーの背景色
    strokeWeight (lweight);//バーの太さ
    line (px,ly,lfx,ly);//バーの背景の描画
    stroke (200,0,0);//バーの色
    line (0,ly,px,ly);//バーの描画
    fill (255,0,0);//ポイントの色
    noStroke ();//輪郭線の削除
    circle (px,ly,pr);//ポイントの描画
    pop ();//なくてもいい(描画スタイルのロード)
  }
  
  boolean pressed=false,drag=false;
  
  float dragPoint (){//ドラッグ
    if (mousePressed&&mouseButton==LEFT&&!pressed){//クリックの瞬間
      if (hoverPoint()){//マウスポインタがポイントをクリック出来ているか
        drag=true;
      }
      pressed=true;
    }
    if (drag&&mousePressed){//ドラッグ中
      px+=mouseX-pmouseX;//x座標でのマウスポインタの移動量
      if (px<lsx){
        px=lsx;
      }
      if (px>lfx){
        px=lfx;
      }
      return px/(lfx-lsx);
    }
    if (!mousePressed){//ドラッグ解除
      pressed=false;
      drag=false;
    }
    return -1;
  }
  
  boolean hoverPoint (){//ポイントに照準があっているか
    if (sqrt(pow(px-mouseX,2)+pow(ly-mouseY,2))<pr){//三平方の定理を利用
      return true;
    }
    return false;
  }
}
```