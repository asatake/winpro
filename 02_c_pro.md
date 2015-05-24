# #02 C言語の環境を整えよう編

C言語を学ぶ環境を整えます。  
あまり難しいことはないので、確実に設定しましょう。

#####今回導入するもの
- __gcc__
- __Atom__

エディタとコンパイラを導入します。  
コンパイラは、書いたプログラムを機械が読み取れるように翻訳するためのものです。  

###1.コンパイラの導入
まずはコンパイラを入れてみましょう。  
都合により2種類入れますが、好きな方を使ってください。

#### #gccの導入
まず一般的なC言語のコンパイラである、gccの導入です。  

Cygwinを開き、以下のどちらかのコマンドでgccの導入は完了です。
```
apt-cyg install gcc
または
choco install gcc
```
インストール確認ですが、以下のコマンドでバージョン情報が出たらOKです。
```
gcc --version
```


###2. エディタの導入
エディタは、今回Atomを導入します。  
Vimを使いたい人は、こちらをどうぞ。  
Vimもお勧めです。

__[>Cygwin使いのVim](vim_set/vim_beg.md)__

では、Atomを導入します。  

1. [Atom公式サイト](https://atom.io/)から、Downloadボタンを押してインストーラをダウンロードし、実行します。  
2. 勝手にインストールされます。
3. Cygwinを開き、次のコマンドを編集して入れてください。
```
git config user.name "自分の名前(英数字)"
git config user.email "自分のメールアドレス"
```

4. また、ホームディレクトリにある.zshrc、または.bashrcを開き、次の一文を入れてください。
```bash
alias atom='cmd /c atom'
```
これで起動しない場合は、Windowsの環境変数に次のパスを追加してみてください。
```bash
C:\Users\ユーザ名\AppData\Local\atom\bin
```
<<<<<<< HEAD
それでもだめなら、上に書いたaliasを次のように変更してください。
```bash
alias atom='cmd /c C:/Users/ユーザ名/AppData/Local/atom/bin/atom.cmd'
```
=======
>>>>>>> parent of dbf03f9... add

5. Cygwinを再帰動し、「atom」と入力して起動してみましょう。  
(以後、Atomを起動するときはCygwinから起動してください。)

これで、とりあえずの環境は整いました。  
もっと使いやすくするために次のようなプラグインを入れるのもいいと思います。  
ただ、少しお重くなったりもするので、お好みで入れてください。

* linter
* linter clang
* autocomplete clang
