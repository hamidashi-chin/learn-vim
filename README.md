# 概要

今まで馴染みのなかった内容についてメモ

# NeoVim
## VimからNeoVimに移行

- .zsh_aliases
```
alias vi="nvim"
alias vim="nvim"
alias view="nvim -R"
```

## コマンドモード

- コマンド実行(例：pythonでtest.pyを実行)
```
:! python3 test.py
```

- 直前のコマンドと同じコマンドを再度実行
```
:!!
```

- コマンドで同じ場所にあるファイル確認する例
```
:!ls
```

## 移動

慣れておいたらコード書く時便利そう😍

- 10行目に移動する例
```
:10
```

- インデントの先頭に移動する
```
^ (キャレット)
```

- 段落ごとに移動
```
{ # 上に移動
} # 下に移動
```

- セクションごとに移動
```
[[ # 上に移動
]] # 下に移動
```

- ファイルの先頭に移動
```
:1 or gg
```

- 移動前の場所に戻る
```
ctrl + o
```

## 検索・置換

- シンタックスのon/off ※検索・置換とあんまり関係ないけど
```
:syntax off # シンタックスOFF
:syntax on  # シンタックスON
```

- /{検索ワード}で検索した際のハイライトのon/off
```
noh or :set nohlsearch # ハイライトOFF
:set hlsearch          # ハイライトON
```

- 置換 ※あんまり使わないけど。カードル上の文字が入力した文字で上書きされていく
```
R
```

- 単語消す ※上記の文字列上書きよりも、単語消してから入力するパターンの方がよく使う
```
dw
```

- 一括置換
```
:%s/{置換対象文字列}/{置換後文字列}/g
```

- 一つずつ確認しながら一括置換 ※置換する場合は`y`置換しない場合は`n`
```
:%s/{置換対象文字列}/{置換後文字列}/gc
```

## Visualモードやインデント

- 空白行つくってINSERTモードに入る
```
o # カーソルの下に空白行
O # カーソルの行に空白行 カーソル上にあった行は一行下にいく こっちの方がよく使う
```

- 下の行と連結する ※下の行をカーソルある行の行末に移動させる
```
J
```

- 指定箇所にインデント入れる
Normalモードの状態からVisualモードになり、インデント入れる行を選択してから
```
> # 右にインデント
< # 左にインデント
```

- 選択した文字列をコピーしてそれをペースト
Visualモードで対象を選択、`y`を押下(yank)してコピーしてから
```
p
```

- まとめて複数行コメントアウトする
Visualモードになってから該当行を選択して
```
:norm I{コメントアウトで使用する文字列} # 行頭に文字列挿入
:norm A{コメントアウトで使用する文字列} # 行末に文字列挿入
```

## Vimのコンフィグ設定

- 貼り付けモード コンフィグと直接関係ないが。Webからコピーしてきたコードを貼り付けるとautoindentによりインデントがおかしくなってしまう場合に下記を行うと勝手なインデントが入らない
```
:set paste
```

```
set shell=/bin/zsh    # デフォルトシェルをzshに設定
set shiftwidth=4      # インデントの幅を指定
set tabstop=4         # タブの幅が半角スペース何個分か指定
set expandtab         # タブ入力した時、タブではなく半角スペース出力されるよう設定
set textwidth=0       # 自動的に折り返される列数を設定 0だと自動的に折り返されなくなる設定
set autoindent        # 新しい行を開始する際に自動的に前の行のインデントが引き継がれる設定
set hlsearch          # 検索したとき対象文字列にハイライトが入る
set clipboard=unnamed # unnamed オプションを設定すると、通常の yanking（ヤンク）や pasting（ペースト）がシステムの "プライマリ" クリップボードを使用する設定
syntax on
```

### nvimの設定ファイルについて

 - ファイルは下記に作成する
```
~/config/nvim/init.vim
```
- dotfilesでGit管理する場合は下記で設定している（自分用）
```
ln -n -s ~/dotfiles/nvim ~/config/nvim
```

## Vimのゲームで操作を覚えていく

[https://vim-adventures.com](https://vim-adventures.com)

# Vimのプラグイン

## Vimのプラグイン管理のVim Plug

Vimのプラグイン管理には下記ある
- Vim Plug
- Vundle
- Pathogen
- Dein
- Janus

最近人気あるVim Plugを使う

### vim-plugのインストール
[https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)

```
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

### nvim.initにvim-plugの設定値の書き方

```
call plug#begin()

〜 ここにいろいろ書く 〜

call plug#end()
```

### vim-holizonをインストールしてみる

- [vim-horizonのGithubページ](https://github.com/ntk148v/vim-horizon?tab=readme-ov-file)

- init.vimの`call plug#begin()`と`call plug#end()`の間に下記を入力
```
Plug 'wesQ3/vim-horizon'
```
- コマンドモードにて下記を実行しインストール実行
```
:PlugInstall
```

## NERDTree

[NERDTree](https://github.com/preservim/nerdtree)

- init.vimに下記追記して`PlugInstall`を実行
```
Plug 'preservim/nerdtree'
```

- インストールできたら下記でNERDTree表示
```vim
:NERDTree
```

- ディレクトリは`Enter`で開き、開いている状態で`Enter`で開いていた状態から閉じた状態になる
- カーソルがファイル名上にある時に`Enter`でファイルを開く
    - ファイル編集側からTree側にカーソルを移動する場合は`ctrl + ww`
    - Tree側からファイル編集側に戻る場合は再度`ctrl + ww`
- ファイル編集側のみ表示してNERDTree側を非表示にする場合は、Tree編集側にカーソルがある状態で`:q`
    - 再度Treeを表示する場合は`:NERDTree`を行う
    - もしくは`:NERDTreeToggle`でも同様にいける
    - ただ、上記を毎回入力するのは面倒なのでinit.vimに下記ショートカットの設定を追記
      ```vim
      nnoremap <leader>n :NERDTreeFocus<CR>
      nnoremap <C-n> :NERDTree<CR>
      nnoremap <C-t> :NERDTreeToggle<CR>
      nnoremap <C-f> :NERDTreeFind<CR>
      ```
    - ファイルを指定せずにnvimを起動した場合はNERDTreeを表示し、ファイル名を指定してnvimを起動した場合はNERDTreeを表示しない設定をinit.vimに追記
      ```vim
      " Start NERDTree when Vim is started without file arguments.
      autocmd StdinReadPre * let s:std_in=1
      autocmd VimEnter * if argc() == 0 && !exists('s:std_in') | NERDTree | endif
      ```

## FuzzyFinder

[FuzzyFinder](https://github.com/junegunn/fzf)

- init.vimに下記追記して`PlugInstall`を実行
```
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
```

インストールできたら下記でfzf起動
```vim
:FZF
```
その後、検索するファイルのキーワードを入力すると候補のファイルが表示れる

