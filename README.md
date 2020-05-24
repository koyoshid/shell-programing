# shell-programing
## シェルプログラムを書くための基本事項
- シェルプログラムの先頭には#!/bin/shを書く
- シェルプログラムには実行権限(xフラグ)を与える

## 1行の取り扱い
- コマンドをコマンドとして区切る働きをするのが「改行コード」である

## ワイルドカード
- \* 文字列全部
- ? 1文字
- [...] [ ]の中に含まれる文字のどれか1つ
- [!...] [ ]に含まれない文字

## 特殊文字
### クォート
- シェルが特殊だと判断する文字の意味を剥奪すること
- エスケープすること
- 利用目的
    - 何かコマンドを実行させるとき
    - 渡す引数をシェルが自動的に解釈しないようにしたいとき

### バックスラッシュ
- 直後の文字の特殊な意味をなくす機能

### シングルクォーテーション
- シングルクォーテーションで囲まれた文字列('...')の中の特殊文字は全て普通の文字と同じ扱いになる

### ダブルクォーテーション
- $ ` \という3つの特殊文字はダブルクォートで囲まれてもエスケープできない
- 上記の3つ以外の特殊文字の意味をエスケープする

### バッククォート
- バッククォートで囲まれた中に書かれたコマンドを実行してその結果をその位置に書き込む

### コマンド終了時のステータス
- コマンドが正しく終了したときに0、そうでない場合に1を終了時にセットする
- 0 成功 true
- 0以外 失敗 false
- コマンドの実行結果は$?という変数にセットされる
```
# echo コマンドで確認できる
echo $?
```

## コマンドセパレータ

### セミコロン
- ;
- 1つのコマンドの区切り
- 改行と同じ
- 複数行にまたがる記述を1行にまとめられること

### パイプ
- |
- 左から右へ流していくパイプライン処理
- 出力された結果を次のコマンドの入力にする

### アンバサダー
- &
- バックグラウンドで実行させる

### OR演算子
- ||
- 左側のコマンドが失敗したとき初めて右側のコマンドを実行するように動作する

### AND演算子
- &&
- 左側のコマンドが成功したときだけ右側のコマンドを実行するように動作する

## コマンドのグルーピング

### 丸括弧
- 現行の状態を変えたくないが、変えた状態で何かをやらなくてはいけないというような場合に利用する
- 括弧で囲まれたコマンド群は現在の動作しているシェルとは別に、サブシェルの元で動作することになる
    - サブシェルとは、今のシェルが新しくシェルを動作させ、その中で動作するもの
- 今のシェルは、そのサブシェルが終了するまで次の処理には移行できない
- 今のシェルとサブシェルは親子関係である。親の環境は子に引き継ぐことはできる。逆に子の環境は親に引き継ぐことはできない。
- 子シェルの中でディレクトリ移動等、環境を変えたりして何らかの処理を行なった場合、親に戻ってきた時に環境は何も変わらないまま元のままの状態をキープする

### 中括弧
- 複数のコマンドの結果をひとまとめにしたい時に使う
- 現行のシェルの中で実行される
- 中括弧の前後にはスペースが必要である
- 中括弧の中の最後のコマンドはセミコロンを打っておかなくてはいけない
```
# 以下のように書くことでスペース、セミコロンを意識せずにかける

{
    command1
    command2
}


```
