# 演習問題 解答例
各章の演習問題の解答例です。

## 目次
1. [変数と定数と標準出力](#1-変数と定数と標準出力)
2. [変数と計算](#2-変数と計算)
3. [制御文](#3-制御文)
4. [配列](#4-配列)
5. [関数](#5-関数)

## 1. 変数と定数と標準出力
問1.
```
void setup (){
  println (PI);
}
```

## 2. 変数と計算
問1.
```
void setup (){
  println (8/3);
}
```

## 3. 制御文
問1.
```
void setup (){
  for (int i=0;i<=45;i+=3){
    println (i);
  }
}
```

## 4. 配列
問1.
```
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
```
int big (int n){
  return n*2;
}
```

問2.
```
void tri (int hei){
  for (int i=0;i<hei;i++){
    for (int j=0;j<=i;j++){
      print ('*');
    }
    println ();
  }
}
```