# Vim

控制台运行 vimtutor 这是 vim 官方实操教程
三种模式：

- 一般模式
- 编辑模式
- 命令行模式

## 光标的移动
### 单词级

- w or W 向移动到下一单词开头  ★★
- b or B 向左移动到单词开头	★★

### 块级

- `gg`文档第一行，相当于1G 	★★★
- `G`文档最后一行,`<n>G`移动到你n行    ★★
- `0`或`home`到行首（第1列）	★★
- `$`或`end`到行尾	★
- `:<N>`or `<n>gg`跳转到第N行	★★★
- `ctrl-f` 屏幕向下移动一页
- `ctrl-b` 屏幕向上移动一页
- `<n>j`或者`<n>↓`，向下移动n行，同理，也可以实现左右移动 ★★★
- `v`或者`V`，字符选择或者行选择 ★★★
- `ctrl-v` 长方形选择，牛逼了 ★★★

> 注意，所有命令都可以加一个数字N，表示对后面的命令执行N次，比如`<n>G`表示移动到第n行。

### 高级移动
- `'.` 跳到最后修改的那一行
- `gd` 跳到当前变量在当前文件的定义处，其实是跳转到当前变量在此文件中第一次出现的地方，不过一般来说，第一次出现的地方也就是变量定义的地方 ★★★
- `ma` 在当前位置做标记，用字母a标记当前光标所在位置，这里a可以是任意字母
- ``a` 跳到标记a处 ★★
- `` 跳到上一次光标所在处，相当有用 ★★★


## 打开文件、查找内容
### vim中打开文件
- `:e <filename>`，在vim中打开名为filename的文件，如果没有，则创建；

### 文档内查找
- `*` 向后查找光标当前所在单词
- `#` 向前查找光标当前所在单词	★★★
- `/<search>` 向后查找指定字符
- `?<search>` 向后查找指定字符串
- `n` 继续查找下一个	★★★
- `N` 继续查找上一个

### 匹配查找
vim 中可以使用` %` 对 `( `和 `)`，`[` 和 `]`，`{ `和 `}` 进行匹配查找，当光标位于其中一个 符号上时，按下` %`，光标会跳到与之匹配的另外一个符号上。

> 括号匹配，程序员必备



## 文档的修改与保存
### 插入
- `a` 当前字符后插入	★★★
- `I` 行首插入
- `A` 行尾插入
- `o` 在下一行插入	★★★
- `O` 在上一行插入	★★★
- `ctrl-p` 插入模式下进行单词补齐，比如有一个变量为`fifth_test_day`，那么你只需要敲入部分名之后，就可以按下`ctrl-p`自动补全了。★★★

### 删除
- `x` 删除当前字符
- `X` 向前删除一个字符，相当于键盘的`Back Space`。
- `dd` 删除当前行，并将删除内容保存在vim剪贴板 `ndd`表示删除光标所在的向下n行。★★
- `dw` 删除光标所在位置到下个字的第一个字母
- `daw` 删除一个单词，包括词尾空格，实用，不用将光标移动到单词第一个字母，`aw`表示`a word`
- `d<X>` 删除指定内容，保存在剪贴板
- `c<X>` 删除指定内容，保存在剪贴板，同时进入insert模式

> 说明，<X>部分是对操作内容的描述，比如，删除一个单词，可以dw或者de，要复制当前位置到行尾内容，可以输入`y$`，要删除后面3个字符并插入，就输入`c3l`。

### 复制
- `yy` 复制当前行到vim剪贴板	`nyy`复制光标向下n行 ★★★
- `y<X>` 复制指定内容到剪贴板

### 粘贴
- `p` 当前位置后粘贴	★★★
- `P` 在当前位置前粘贴

### 合并
- `J` 当前行与下一行合并

### 替换
- `r<X>` 将当前字符替换为X  ★★★
-  `:%s/search>/<replace>/` 查找search内容并替换为replace内容，正则表达来替换，这个命令可以消除所有行位多余的空格：`:%s/\s\+$//`	★★★
- `<n1>,<n2>s/word1/word2/gc` n1/n2都是数字，在`n1`行和`n2`行之间寻找`word1`，替换为`word2`。`c`代表`confirm`，替换前需要你确认，不加就默认全部替换。`n2`用`$`表示时，表示搜索到最后一行。★★★

### 撤销、重做

- `u` 撤销	★★★
- `ctrl-r` 重做 ★★★
- `.` 重复前一个操作的意思 ★★★

### 保存文件
- `:wq` or `ZZ` 保存并推出
- `:q!` or `ZQ` 强制推出，不保存
- `saveas <newfilename>` 文件另存为

### 编辑
- `ctrl-n` Vim自带的补全（按照全文已有输入）★★★

## 多窗口
- `:sp` 切割窗口
- `ctrl-w-j`或者`ctrl-w-↓` 跳转窗口
- `:q`或者`ctrl-w-q` 关闭当前窗口


## 设置vim
为了让vim使用起来更加得心应手，先做一些简单的配置。

编辑VIM配置文件，可能一开始没有这个文件，不过没关系，直接`vi ~/.vimrc`保存这个文件即可。

### 简单设置vim：
```
set number """显示行号
set relativenumber """显示相对行号（这个非常重要，慢慢体会）
set hlsearch """搜索结果高亮
set autoindent """自动缩进
set smartindent """智能缩进
set tabstop=4 """设置 tab 制表符所占宽度为 4
set softtabstop=4 """设置按 tab 时缩进的宽度为 4
set shiftwidth=4 """设置自动缩进宽度为 4
set expandtab """缩进时将 tab 制表符转换为空格
filetype on """开启文件类型检测
syntax on """开启语法高亮
```

关于vim的配置，还可以看[强大的vim配置文件，让编程更随意](http://www.cnblogs.com/ma6174/archive/2011/12/10/2283393.html)


### 重复上一次命令
vim有一个特殊的命令`.`，你可以用它重复执行上一个命令。我感觉有点像EXCEL中的`F4`命令。

### 缩进
- `>>` 向右缩进当前行
- `<<` 向左缩进当前行

## 分屏与标签页
### 分屏方式

- `:split` 缩写`sp` or `ctrl-w s`上下分屏
- `:vsplit` 缩写`vs` or `ctrl-w v`左右分屏
- `:diffsplit` 缩写`:diffs` diff模式打开一个分屏，后面可以加上{filename}

### 窗口跳转

- `ctrl-w w` 激活下一个窗口
- `ctrl-w j` 激活下方窗口
- `ctrl-w k` 激活上方窗口
- `ctrl-w h` 激活左侧窗口
- `ctrl-w l` 激活右侧窗口

## 插件
采用[vim-plug](https://github.com/junegunn/vim-plug)安装、升级、管理插件。

添加 vim-plug 的配置到 `~/.vimrc` 中：

- 配置以 `call plug#begin()` 开始
- 插件列表，以 Plug 命令开头
- 用 call plug#end() 结束，以初始化插件系统
这将会自动开启 `filetype plugin indent on` 和` syntax enable`，如果不希望这 样，你可以在该配置后重置你的设置，例如：`filetype indent off, syntax off`

### 安装vim-plug
先`cd ~`，然后创建`mkdir .vim`，接着执行如下命令：
```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
会在~/.vim文件夹下创建autoload文件夹，同时将下载的plug.vim文件归档到该文件夹下。
下面是官方对`~/.vimrc`文件配置的一个Example:
```
" Specify a directory for plugins
" - For Neovim: ~/.local/share/nvim/plugged
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.vim/plugged')

" Make sure you use single quotes
" 注意要使用单引号

" Shorthand notation; fetches https://github.com/junegunn/vim-easy-align
" 如果插件在 GitHub 的地址是 https://github.com/junegunn/vim-easy-align
" 可以缩写成下面这样
Plug 'junegunn/vim-easy-align'

" Any valid git URL is allowed
" 或者直接给定插件 git 地址
Plug 'https://github.com/junegunn/vim-github-dashboard.git'

" Multiple Plug commands can be written in a single line using | separators
" 多个 `Plug` 命令可以写在一行，用 `|` 符号分割
Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

" On-demand loading
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Using a non-master branch
Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

" Using a tagged release; wildcard allowed (requires git 1.9.2 or above)
Plug 'fatih/vim-go', { 'tag': '*' }

" Plugin options
Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }

" Plugin outside ~/.vim/plugged with post-update hook
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }

" Unmanaged plugin (manually installed and updated)
Plug '~/my-prototype-plugin'

" Initialize plugin system
call plug#end()
```

### vim-plug常用命令

常用命令
|命令	|说明|
|-----|-----|
|PlugInstall [name ...] [#threads]|	安装插件|
|PlugUpdate [name ...] [#threads]|	安装或升级插件|
|PlugClean	|清理插件|
|PlugUpgrade	|升级 vim-plug|
|PlugStatus|查看已安装插件的状态|

### 怎么使用这些命令呢？

直接`vim`之后，进入冒号的命令模式，输入上述命令就可以执行命令了。

## FAQ

### Q1:配置VIM，安装vim-plug插件之后，想要生效通过`source ~/.vimrc`命令生效配置，就会报错：`E492: Not an editor command: Plug`

```
[root@localhost ~]# source .vimrc
-bash: .vimrc: line 2: syntax error near unexpected token `('
-bash: .vimrc: line 2: `call plug#begin('~/.vim/plugged')'
```

A：- [error while running “source .vimrc”](https://stackoverflow.com/questions/21651114/error-while-running-source-vimrc)
原因是，我们`.vimrc`本身并不是shell文件，而`source ~/.vimrc`等价于`./.vimrc`，当然后校验shell语法了。看了StackOverflow上的解答才清楚的。
- 可以通过输入`$vim`直接进入vim的命令模式，执行下面命令
```
:source ~/.vimrc
```
注意，我这里`.vimrc`的位置就是位于`~`目录下，你可以`:source /path/to/.vimrc`

- 或者编辑完`.vimrc`文件，直接：
```
:so $MYVIMRC
```

### Q2:从Win上复制文件时，常常因为换行符出错：

```
:set fileformat=unix
```

A：
linux的文件换行符为`\n`，但windows却非要把`\r\n`作为换行符，所以，vim在解析从windows拷贝到linux的的vimrc时，因为遇到无法解析的\r，所以报错。

- [vim E492: Not an editor command: ^M(使用VIM打开文件一直提示错误)](http://blog.csdn.net/yin_pengpeng/article/details/51674064)

## 参考

- [dofy/learn-vim](https://github.com/dofy/learn-vim)
- [Vim 实操教程（Learn Vim）](https://github.com/dofy/learn-vim)
- [vim环境设定：~/.vimrc(语法高亮等一些的设置)](http://blog.csdn.net/u013412790/article/details/51673333)
- [无香花自开-Vim配置](https://blog.csdn.net/qdx411324962/article/details/49685151)
- [那些离了就活不了的 VIM 插件](http://www.zlovezl.cn/articles/vim-plugins-cannot-live-without/)