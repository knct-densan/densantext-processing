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
    for (int j=0;j<=i;j++){
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

int n;
```

## 7. 画面の描画がしたい
問1.
```java
void setup (){
  size (500,500);
  background (255);
}
```
問2.
```java
void setup (){
  fullScreen ();
}

int i=0;

void draw (){
  background (255);
  fill (255,0,0);
  rect (width/2-150+i++,height/2-150,300,300);
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
  switch (++pressNum%4){
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
  circle (mouseX,mouseY,20);
}
```

問3.
```java
void setup (){
  size (500,500);
}

void draw (){
  if (mouseX>100&&mouseX<400&&mouseY>100&&mouseY<400){
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
ArrayList<Character> buf=new ArrayList();

void draw(){
}

void keyTyped (){
  buf.add(key);
  if (key=='\n'){
    for (char c:buf){
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
    buf.setLength(0);
  }
}
```

## 10. クラスを自作する
問1.
```java
class Student{
  int grade,group,number;
  String name;
  
  Student (int grade,int group,int number,String name){
    this.grade=grade;
    this.group=group;
    this.number=number;
    this.name=name;
  }
  
  void getInfo (){
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
    return new Sample (id,size);
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
  image (img,x,y,img.width*a,img.height*a);
}
```