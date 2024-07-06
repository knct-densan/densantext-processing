# 音声データを使う(Minimライブラリの使用)
precessingで音声データを扱う場合には様々な方法があるが、本テキストでは比較的簡単に実装できるMinimライブラリを使用する。

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
この文字列は