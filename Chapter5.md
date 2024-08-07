# 関数
この章では今まで使ってきた関数を自分で作る方法を学ぶ。

## 目次
* [関数とは](#関数とは)  
* [返り値](#返り値)  
* [関数名](#関数名)  
* [引数](#引数)

## 関数とは
関数とは機能を持った命令である。
関数には以下のように宣言できる。
```java
返り値の型 関数名 (型 引数1,型 引数2, ...){
    処理
}
```
つまりsetupも関数の一つである。  
呼び出す場合は`関数名 (引数1,引数2, ...)`のようにして呼び出せる。

## 返り値
返り値は関数の実行結果として返却される値である。  
返り値を返す際は`return 返り値;`のように記述する。返り値がない場合でもreturnは使用でき、`return;`のように書くことができる。returnが実行されると関数はそこで終了する。  
返り値を持つ関数を作る場合必ず値を返さなければならない。  
返り値がない関数の場合、返り値の型は`void`を使う。

返り値を持つ関数には`sqrt()`や`sin()`等が挙げられる。

## 関数名
関数の名前は基本的にかぶってはいけない。しかし、同じ名前の関数であっても引数の数や並びが違う場合、呼び出されたときprocessing側が判断して引数の数や並びが等しい関数を呼び出すため宣言することができる。  
このように同じ名前の関数を宣言することをオーバーロードという。

オーバーロードの例(引数の数が違う)
```java
void setup (){
  sum (1,2,3);//関数の呼び出し
}

int sum (int a,int b){
  return a+b;
}

int sum (int a,int b,int c){//こちらが呼び出される
  return a+b+c;
}
```

## 引数
引数は関数が処理に使うための値である。例を挙げるとprintln関数に渡す表示内容が挙げられる。

引数を作るときは型と引数名を付けて作成できる。引数を二つ以上取りたいときはコンマ区切りで引数を宣言すればよい。

関数を呼び出すときに渡す引数の数は、関数の宣言時に宣言した引数の数でないと実行できない。
```java
void setup (){
  push (3,4,5);//引数の数が違うため実行できない
}

void push (int a,int b){//引数を二つ宣言
  println (a);
  println (b);
}
```
しかし、可変長引数という機能が存在し、受け取る変数の数を指定しないこともできる。可変長引数で受け取った引数は通常の配列として扱う。また、可変長引数は引数の最後にしか書けない。
```java
void test (char c,int... n){//これはできる
}

void test (int... n,char c){//これはできない
}

void test (char... c,int... n){//これもできない
}
```

可変長引数をとる関数の使用例
```java
void setup (){
  push (3,4,5);
}

void push (int... n){
  for (int i:n){
    println (i);
  }
}
```
実行結果
```
3
4
5

```
また、引数に渡されるのは値だけであるため注意が必要である。
```java
void setup (){
  int n=0;
  setVal (n);
  println (n);
}

void setVal (int num){
  num=5;
}
```
実行結果
```
0

```

## 演習問題[^1]
問1. 引数として受け取った整数を2倍にして返す関数`int big (int n)`を作成せよ。

問2. 次の例のように入力された高さの三角形を出力する関数`void tri (int hei)`を作成せよ。  
例.  
入力
```
3
```
出力
```
*
**
***

```
入力
```
5
```
出力
```
*
**
***
****
*****

```

[^1]: 演習問題の解答例は[ここ](answers.md)