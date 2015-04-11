# #01 Cygwinの導入編
_ _ _

どの言語をやるにあたっても必要になるソフトの導入をしてしまおうと思います。  
正直、この作業が一番大変かもしれません。(時間かかるし)  
ここで心が折れてしまいそうですが、頑張りましょう！

あと、今回かなり文章も長いです。根気よくいきましょう。

#####今回導入するもの
* __Cygwin__

いわゆるターミナルを使うために導入します。  
Windowsに最初から入っている「コマンドプロンプト」だと色々と不便なことがあったり、  
出来ないことがあったりするので、別途コマンドラインをインストールします。  
最初に入れるソフトにして、一番扱いが難しいソフトウェアだと思います。  
しかし、ちゃんと使いこなせればとても便利です。

では、導入してみましょう。

<目次>  
1. [インストール](#1.インストール)
2. [設定(.minttyrc)](#2.設定(.minttyrc))
3. [bashの設定(.bashrc)](#3.bashの設定(.bashrc))
4. [開いて確認してみよう](#4.開いて確認してみよう)
5. [zshの設定とoh_my_zshの導入](#5.zshの設定とoh_my_zshの導入)
6. [apt-cygとchocolateyの導入](#6.apt-cygとchocolateyの導入)

####1.インストール

1. まず、[Cygwin公式サイト](https://www.cygwin.com/)にアクセスします。  
2. 左側のメニューから「Install Cygwin」をクリックします。  
3. ここで使用PCが  
 - 32bitの場合は32bit versionsの「setup-x86.exe」
 - 64bitの場合は64bit versionsの「setup-x86_64.exe」

 をクリックし、ダウンロードします。(このファイルは要保管)

これで、とりあえず準備は出来ました。ここからCygwinをインストールします。  
1. DLしたファイルを実行したら、とりあえず「次へ」を選択します。  
2. 「Install from Internet」を選択して「次へ」。  
3. 特に困ることがない限りは「C:\cygwin64」入れてしまいましょう。というわけで、「次へ」。  
4. これも特に問題なければそのまま「次へ」。  
5. 個人的に「Direct Connection」がいいと思うので、選択して「次へ」。  
6. 日本のサーバのほうが安定すると思うので末尾が「ac.jp」で終わってるアドレスを選択して「次へ」。  
7. 左上の「search」と書いてあるボックスに必要なパッケージを入力します。  

さて、ここで今回入れるパッケージですが、とりあえず次のものを入れておきます。
- wget(必須)
- gnupg(必須？)
- gawk(必須？)
- zsh(今後解説)
- git(便利)

他に追加したいものがあれば、いつでもここからパッケージを入れることができます。

では、これらを左上のsearchに入力してみましょう。  
そして画像の赤い枠のところを「Install」と表示されるまでクリックしましょう。

![cyg_inst](img/cyg_inst.png)

他のパッケージも同様にして「Install」にしたら、「次へ」を押します。  
すると、ここからインストールが開始します。  
初回は長いとは思いますが、辛抱して待ちましょう。

インストールが終わると、
- デスクトップにアイコンを作るか
- スタートメニューにCygwinを登録するか

の選択肢が出ます。これはお好みでどうぞ。
_ _ _

####2.設定(.minttyrc)

ここからが本当の闇だ。

というのは冗談ですが、ここからは結構面倒くさいかもしれません。  
ここで書くのはあくまで一例なので、必要に応じてググるのもいいと思います。  

ここで重要な事なのですが…  
__この先は「サクラエディタ」をインストールしていることを推奨します。__  
サクラエディタ公式サイトは[__こちら__](http://sakura-editor.sourceforge.net/)  
そうでもしないと設定ファイルを書き換える手段が難しくなります…。

また、Vimというテキストエディタもおすすめです。  
Cygwin上で開けるので、慣れるとこちらのほうが早いかもしれません。
設定方法はこちらから。  
__[>Cygwin使いのVim](vim_set/vim_beg.md)__

1. Cygwinをインストールしたフォルダに移動します。  
（何もいじっていなければ"C:\cygwin64"のはず）  
2. そこから、Home -> (ユーザ名の書かれたフォルダ)と開いていきます。  
3. .minttyrcというファイルを開く、または作成します。  

この.minttyrcとは、Cygwinの見た目を変更するものです。  
変えない場合はこのままでどうぞ。  

_（注）.minttyrcというのは拡張子のように見えますが、こういうファイル名です。  
なので「.」以前に何か文字を入れると機能しなくなりますのでご注意を。_  

例えば私の場合、このファイルにはこう書かれています。（括弧内は書いてませんが補足説明です）
```bash
Locale=ja_JP  (言語設定？)
Charset=utf-8  (文字コード)
Font=Mgen+ 2m regular (フォントの設定、お好みで)
FontHeight=11　(フォントサイズ)
FontIsBold=no　(フォントを太字にするかどうか)
BackgroundColour=0,0,0　(背景色、ここでは黒)
ForegroundColour=255,255,255　(文字色、ここでは白)
CursorColour=255,255,255　(カーソルの色、ここでは白)
OpaqueWhenFocused=no　(よくわからない)
Transparency=40　(Cygwinのウインドウをどれだけ透過するか)
```
_ _ _
####3.bashの設定(.bashrc)
先ほどの.minttyrcと同じフォルダで作業します。  
.bashrcとほ、コマンドライン自体の設定です。  
こっちのほうが複雑ですので、以下の例をそのまま使っていいと思います。  
ただ、それで物足りなくなる場合は、随時追加していきましょう。

_（注）.bashrcというのは拡張子のように見えますが、こういうファイル名です。  
なので「.」以前に何か文字を入れると機能しなくなりますのでご注意を。_

1. Cygwinをインストールしたフォルダに移動します。  
（何もいじっていなければ"C:\cygwin64"のはず）  
2. そこから、Home -> (ユーザ名の書かれたフォルダ)と開いていきます。  
3. .bashrcというファイルを開く、または作成します。  
4. 以下のように記述し、保存してください。

```bash
# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

ulimit -c 0
umask 022
set history=200
set savehistory=200
set -o ignoreeof
unset autologout

export SHELL=/bin/bash
export HOME=/home/UserName (UserNameには自分のユーザー名を入れます)
export TMPDIR=/tmp
export TZ=JST-09
export MAKE_MODE=unix

# PATH Setting
PATH="/usr/bin"
export PATH="/bin:$PATH"
export PATH="/usr/local/sbin:$PATH"
export PATH="/usr/sbin:$PATH"
export PATH="/sbin:$PATH"
export PATH="/usr/local/bin:$PATH"
export PATH="/cygdrive/c/Windows/System32:$PATH"

PAGER=less
JLESSCHARSET=japanese-sjis
export PATH PAGER JLESSCHARSET

PS1="$HOSTNAME:\w$ "

if [ -n ${DISPLAY} ]; then
    export DISPLAY=localhost:0.0
fi

if [ ! -n "${TERM}" ]; then
    TERM=cygwin
fi

# Windows System
SYSTEM=`cygpath -u ${SYSTEMROOT}`/system32
alias ping="$SYSTEM/ping.exe"
alias arp="$SYSTEM/arp.exe"
alias nslookup="$SYSTEM/nslookup.exe"
alias traceroute="$SYSTEM/tracert.exe"
alias route="$SYSTEM/route.exe"
alias netstat="$SYSTEM/netstat.exe"
alias ipconfig="$SYSTEM/ipconfig.exe"
alias ifconfig=ipconfig
#alias start="$SYSTEM/CMD.exe /c start"
alias start=cygstart

# alias
alias ls="ls -F --color=auto --show-control-char"
alias la="ls -aF"
alias ll="ls -l"
alias j=jobs
alias vi=vim
alias more=less
alias restart='exec $SHELL -l'

unset SYSTEM
```
#####補足
ここで書いた'export PATH'というものは、PATH(パスと読む)を追加しています。  
PATHは、ホームディレクトリからそのファイルの場所までの道のり、といった感じのものです。

また、aliasというのは、そのコマンドを打った時に何をするかを設定するものです。
私の例で、一番下の方に`alias restart='exec $SHELL -l'`というのを入れましたが、  
これはcygwinの設定ファイルを読み込み直すためにcygwinのシステムを開きなおしています。  
毎回`exec $SHELL -l`と書くのは面倒だし、覚えられないので、  
'restart'とコマンドを打つとそれを実行するように設定しています。

_ _ _

####4.開いて確認してみよう

では、ここまで書いたらCygwinを起動してみましょう。  
(別に2，3の過程をやってない状態で開いても支障はないです)  
無事、何事もなく開けたらひとまず導入成功です。  
初回起動時にはなにか文章が出ますが、初回だけですので気にしないでください。  

画面には、
```
UserName:~$
```
と書かれているはずです。(UserNameには自分のユーザ名)  
これは、自分が今どのディレクトリにいるのかを表しています。  
一番最初にいる場所を、ホームディレクトリと呼びます。

この右側にコマンドを打つことができ、これによって色々な操作を行います。  
これがコマンドラインの特徴です。  
Windows付属のコマンドプロンプトも似たような感じですね。  
最初は慣れないと思いますが、どんどん使って慣れていきましょう！
_ _ _

####5.zshの設定とoh_my_zshの導入

このままでも十分使えるのですが、処理が軽く、使い勝手が個人的に良いと思うzshを使いたいと思います。
先ほどCygwinのインストールの時にさらっとzshを入れました。  
一度コマンドで「zsh」と打って実行するとどんなものなのかわかると思います。  

このままだとちょっと見づらいので、まずはテーマを設定して見やすくしたいと思います。  
今回は、oh_my_zshを導入します。

1. Cygwinを開いたら、次のコマンドを入力します。
```
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```
2. 終わったら次のコマンドを入力します。
```
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
3. .bashrcと同じように、ホームディレクトリ上に.zshrcというファイルを作成、または編集します。  
_（注）.zshrcというのは拡張子のように見えますが、こういうファイル名です。  
なので「.」以前に何か文字を入れると機能しなくなりますのでご注意を。_
4. もともとファイルがあった場合、なにかいろいろ書いてあって難しいので、一番下に以下を記述します。  
(これは.bashrcに書いたものとほぼ同じです)

```bash
# Windows System
SYSTEM=`cygpath -u ${SYSTEMROOT}`/system32
alias ping="$SYSTEM/ping.exe"
alias arp="$SYSTEM/arp.exe"
alias nslookup="$SYSTEM/nslookup.exe"
alias traceroute="$SYSTEM/tracert.exe"
alias route="$SYSTEM/route.exe"
alias netstat="$SYSTEM/netstat.exe"
alias ipconfig="$SYSTEM/ipconfig.exe"
alias ifconfig=ipconfig

# alias
alias ls="ls -F --color=auto --show-control-char"
alias la="ls -aF"
alias ll="ls -l"
alias j=jobs
alias more=less
#alias start="$SYSTEM/CMD.exe /c start"
alias start=cygstart
alias open=cygstart
alias vi=vim
alias restart='exec $SHELL -l'
```

ここで、一度cygwinを閉じて、もう一度開きます。(設定ファイルを読み込み直します)
zsh自体の設定はできたので、cygwinを開いた時に自動でzshを開くように設定します。
1. `mkpasswd -l > /etc/passwd`というこコマンドを入力します。
2. C:\cygwin\etcにあるpasswdというファイルを編集します。  
(viを使う方は`vi /etc/passwd`で開きます)
3. 'bash'と書いてあるところを'zsh'と書き換えて保存します。
4. cygwinを再起動します。

これで、zshが開いたら成功です。  
(確認方法は、'bash'と入力してbashが開き、'exit'と入力してcygwinが閉じなければ成功です)

次に、テーマを変えます。  
以下のリンク先にサンプルがあるので、好きなデザインを選んでください。  
[Themes - robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)  
そして、.zshrcを開き、以下の箇所を変更します。
```
ZSH_THEME="自分の選んだテーマ名"
```
筆者の場合はgentooというテーマを選んだので、`ZSH_THEME="gentoo"`となっています。  
cygwinを再起動して、テーマが変わっていたら成功です。

#####補足
今回zshを選んだのは、動作の軽さと、コマンドの強力な補完機能があるからです。  
コマンドを打ちたいけど最初の2文字しか覚えてない…となってしまっても、  
`Tab`キーを押すことで、その文字を含む候補を表示してくれますし、  
`Tab`キーを2回押すことで、その保管の中からカーソルを動かして選択することができます。  
コマンドは全て覚えられるわけではなく、また今回は初心者向けということなので、  
zshの方がお勧めなのです。
_ _ _
####6.apt-cygとchocolateyの導入

最後に、パッケージ管理システムを導入します。  
なにか新しい要素(パッケージ)をCygwinに導入するのに、いちいちsetup.exeを開いて…とやるのは面倒です。  
なので、これをCygwinのターミナル上でできるようにします。
