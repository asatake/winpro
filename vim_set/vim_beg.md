#Cygwin使いのVim設定
_ _ _

Cygwin上でVimというテキストエディタの導入方法を紹介します。  
メモ程度ですので、必要に応じて自分で調べてみてください。

導入は、CygwinのSetupに用いたファイルから、wgetなどと同じように入れるか、  
apt-cygコマンドで。  

1. Cygwin上で"vi"と入力する。
2. vimが開きます。

基本はこれだけですが、このままだと不便なので適当にカスタマイズします。

ホームディレクトリ直下に.vimrcというファイルを作り、
そこにこんな記述をします。
```
set nocompatible
filetype off

filetype indent on
syntax on
""矢印キー有効化
let &t_ti.="\e[1 q"
let &t_SI.="\e[1 q"
let &t_EI.="\e[1 q"
let &t_te.="\e[1 q"
""左の括弧を入れたら右の括弧も自動で出す
inoremap { {}<LEFT>
inoremap [ []<LEFT>
inoremap ( ()<LEFT>
inoremap " ""<LEFT>
inoremap ' ''<LEFT>
vnoremap { "zdi^V{<C-R>z}<ESC>
vnoremap [ "zdi^V[<C-R>z]<ESC>
vnoremap ( "zdi^V(<C-R>z)<ESC>
vnoremap " "zdi^V"<C-R>z^V"<ESC>
vnoremap ' "zdi'<C-R>z'<ESC>
""tab押すと空白4つ分インデントできる
set tabstop=4
set shiftwidth=4
set autoindent
""バックスペースで前の文字を削除
set backspace=start,eol,indent
""文字コードは当然UTF-8
set fileencoding=utf-8
""行数も表示しちゃう
set number
set et
set splitbelow

```
これでWindows慣れしてる人でもある程度扱いやすいものになると思います。  
見た目のカラーが見難いと思ったら、Syntaxを変えるといいと思います。

使い方についてですが、こちらのサイトが参考になります。
見ながら覚えていきましょう。

[vim入門(全18回)/ドットインストール](http://dotinstall.com/lessons/basic_vim)  
[Vimの使い方/OCN](http://www15.ocn.ne.jp/~tusr/vim/vim_text0.html)

カーソルの移動は、さっきの設定で矢印キーでもできるようにしたので、そちらでも構いません。
_ _ _

私の.vimrcを晒しておくので参考までに。  
パクってもいいと思います。  
不安な人は適宜ググってください。  
自動補完機能(autocomplete)を使う場合は、一応
```
apt-cyg remove vim
apt-cyg install vim
```
とか打って最新版(Vim7.4)にしておく必要があります。
以下、私の.vimrc。

```
set nocompatible
filetype off

if has('vim_starting')
  set runtimepath+=~/.vim/bundle/neobundle.vim
  call neobundle#begin(expand('~/.vim/bundle/'))
endif
runtime bundle/vim-pathogen/autoload/pathogen.vim

" originalrepos on github
NeoBundle 'Shougo/neobundle.vim'
NeoBundle 'Shougo/vimproc'
NeoBundle 'VimClojure'
NeoBundle 'Shougo/vimshell'
NeoBundle 'Shougo/unite.vim'
NeoBundle 'Shougo/neosnippet'
NeoBundle 'Shougo/neosnippet-snippets'
NeoBundle 'jpalardy/vim-slime'
NeoBundle 'scrooloose/syntastic'
""NeoBundle 'https://bitbucket.org/kovisoft/slimv'
NeoBundle 'thinca/vim-quickrun'
NeoBundle 'nathanaelkane/vim-indent-guides'
NeoBundle 'Yggdroot/indentLine'
NeoBundle 'cohalz/c.vim'
NeoBundle 'Shougo/vimfiler'
NeoBundle 'vim-scripts/java.vim'
NeoBundle 'davidhalter/jedi-vim'
NeoBundle 'Shougo/neocomplete'

let g:quickrun_config={'*': {'split': ''}}
""set list lcs=tab:\|\  
let g:indentLine_color_term = 240
""let g:indentLine_color_gui = '#AAAAAA'
let g:indentLine_color_gui = 'gray'
let g:indentLine_char = '|'

""Vimfiler
autocmd VimEnter * VimFiler -split -simple -winwidth=30 -no-quit
let g:vimfiler_safe_mode_by_default = 0
let g:unite_enable_start_insert = 0
""autocmd BufNewFile *.c 0r $HHOME/.vim/template/c.txt
""autocmd BufNewFile *.vim 0r  put=''

""neocomplete
let g:neocomplete#enable_at_startup = 1
let g:neocomplete#enable_ignore_case = 1
let g:neocomplete#enable_smart_case = 1


filetype plugin indent on     " required!
filetype indent on
syntax on
colorscheme asataken-syntax
let &t_ti.="\e[1 q"
let &t_SI.="\e[1 q"
let &t_EI.="\e[1 q"
let &t_te.="\e[1 q"
inoremap { {}<LEFT>
inoremap [ []<LEFT>
inoremap ( ()<LEFT>
inoremap " ""<LEFT>
inoremap ' ''<LEFT>
vnoremap { "zdi^V{<C-R>z}<ESC>
vnoremap [ "zdi^V[<C-R>z]<ESC>
vnoremap ( "zdi^V(<C-R>z)<ESC>
vnoremap " "zdi^V"<C-R>z^V"<ESC>
vnoremap ' "zdi'<C-R>z'<ESC>
set tabstop=4
set shiftwidth=4
set autoindent
set backspace=start,eol,indent
set fileencoding=utf-8
set number
set et
set splitbelow

NeoBundleCheck
call neobundle#end()
```

なお、colorscheme asataken-syntaxについてですが、  
256-jungleを自分好みにカスタマイズしたものです。  
こちらからどうぞ。  
[asataken-syntax](vim_set/asataken-syntax.vim)  
これも、見づらいと思ったら自分でいじっちゃっていいと思います。  
これについては解説しませんので、他の記事を参考にしてください。
