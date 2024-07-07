# 音声データを使う(Minimライブラリの使用)
precessingで音声データを扱う場合には様々な方法があるが、本テキストでは比較的簡単に実装できるMinimライブラリを使用する。

## 目次
* [Minimライブラリの導入](#minimライブラリの導入)
* [Minimクラス](#minimクラス)
* [効果音の使用](#効果音の使用)
* [bgmを流す](#bgmを流す)
* [演習問題](#演習問題1)

## Minimライブラリの導入
processingでライブラリを導入する際は、ウィンドウ上部の`スケッチ>ライブラリをインポート`からMinimをインポートする。  
Minimがない場合は以下の手順に従ってインストールする。

インストール手順
* ウィンドウ上部の`スケッチ>ライブラリをインポート>Manage Libraries...`を選択。
* 検索ボックスに導入したいライブラリを入力。
* ライブラリを選択し、画面右下の`install`ボタンをクリック。

今回検索ボックスにはMinimと入力する。

インストールが完了したら先述した手順でMinimをインポートする。

## Minimクラス
さて、Minimをインポートすると以下ような文字列が表示されたと思う。
```java
import ddf.minim.*;
import ddf.minim.analysis.*;
import ddf.minim.effects.*;
import ddf.minim.signals.*;
import ddf.minim.spi.*;
import ddf.minim.ugens.*;
```
この文字列はMinimを使うために必要であるため、消さないこと。

音声を扱う準備としてMinimクラスのインスタンスを生成しておく。
```java
Minim minim=new Minim (this);
```
以降の例では上記のように宣言してあるものとして記述していくため、注意すること。

## 効果音の使用
効果音を使用する際はAudioSampleクラスを使うとよい。音声ファイルの読み込みはMinimクラスのloadSampleメソッドを利用する。
```java
AudioSample sample=minim.loadSample ("ファイルのパス");
```
音声の再生にはAudioSampleクラスのtriggerメソッドを用いる。
```java
sample.trigger ();//音が鳴る
```

例. 画面をクリックするたびに効果音が流れる。
```java
import ddf.minim.*;
import ddf.minim.analysis.*;
import ddf.minim.effects.*;
import ddf.minim.signals.*;
import ddf.minim.spi.*;
import ddf.minim.ugens.*;

Minim minim=new Minim (this);
AudioSample sample;

void setup (){
  sample=minim.loadSample ("ファイルのパス");//必要に応じて変更
}

void draw(){
}

void mousePressed (){
  sample.trigger ();
}
```

## bgmを流す
再生を止めたり、サイズが大きい音源を扱う場合はAudioPlayerクラスを使用する。  
読み込み等はAudioSampleとほぼ同じである。

例. 読み込み
```java
player=minim.loadFile ("ファイルのパス");
```
例. 再生
```java
player.play();
```
AudioPlayerクラスはplayメソッドを実行した場合、現在の再生位置から再生され、多重に再生はされない。また、isPlayingメソッドで再生中かどうかを確認できる。

pauseメソッドを実行すると再生が一時停止することができるが、再生位置はリセットされない。

そのため再生位置をリセットする場合、rewindメソッドを使用する。

例. 画面をクリックするたびに再生と停止を切り替え。再生が終わっていた場合、再生位置をリセットする。
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
}

void draw(){
}

void mousePressed (){
  if (player.isPlaying ()){//再生中か否か
    player.pause ();
  }else{
    if (player.position()==player.length()){
      player.rewind ();
    }
    player.play ();
  }
}
```
また、rewindメソッドの代わりに再生位置を変更する、cueメソッドを使用する方法もある。

例. 上の例をcueで書き換えたもの
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
}

void draw(){
}

void mousePressed (){
  if (player.isPlaying ()){//再生中か否か
    player.pause ();
  }else{
    if (player.position()==player.length()){
      player.cue (0);//ミリ秒で再生位置を指定
    }
    player.play ();
  }
}
```
現在の再生位置を取得できるpositionメソッドやファイルの再生時間を取得するlengthメソッドを利用して自身で疑似的にループ区間を設定することができる。

また、playメソッドの代わりにloopメソッドを使用することでループ再生も可能である。

## 演習問題[^1]
問1. スペースキーで再生/停止の切り替え、左の矢印キーで再生位置を10秒戻し、右の矢印キーで再生位置を10秒進めることができるプログラムを作成せよ。  
ウィンドウのサイズは`600×600`、背景は白、再生中には`play`、停止中には`stop`とテキストサイズ`50`で画面中央にテキストを表示すること。なお、再生にはloopメソッドを利用する。  
また、矢印キーの操作は再生位置の先頭と最後尾がつながっているものとして行う。
なお、プログラム開始時には再生は行われていないものとする。

問2. 問1のプログラムに幅が`10`のシークバーを追加せよ。シークバーの再生位置を示す地点には、半径`10`の円をつけること。バーの色は`(R,G,B)=(200,200,200)`、再生済みのバーの色が`(R,G,B)=(200,0,0)`、再生地点を示す円が`(R,G,B)=(255,0,0)`である。  
シークバーの円をドラッグすると再生位置を変更することができ、ドラッグしている最中は再生が停止されるものとする。  
なお、line関数で描画されるラインの色を変更する際はstroke関数を、ラインの幅を変更するにはstrokeWeight関数を使うとよい。また、図形の輪郭線が邪魔な時はnoStroke関数を使うとよい。

[^1]: 演習問題の解答例は[ここ](answers.md)