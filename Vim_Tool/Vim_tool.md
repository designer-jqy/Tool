# vim

## 基本命令

**正常模式下的命令**
`x`：剪切

1. `nx`剪切光标右边n个字符
2. `nX`剪切左边

`d`：删除

1. `dnw`剪切n个单词
2. `dnl`剪切右边n个单词
3. `dnh`剪切左边n个单词
4. `dd`剪切一行

`y`：复制

1. `ynw`复制n个单词
2. `ynl`复制右边n个单词
3. `ynh`复制左边n个单词
4. `yy`复制一行

`p`：粘贴

`r`  进入替换模式
`i`  在正常模式下，按i进入插入模式
`v`  在正常模式下，按v进入视图模式
`：` 在正常模式下，按：进入命令模式

`%！xxd`：显示二进制

## 复制

### 跨文件复制

1. vim打开A文件
2. 普通模式，输入：":sp"或者":vsp"切分出另一个窗口
3. 普通模式，输入：":e B"，在一个窗口中打开B文件
4. 按ctrl+w，按w，切换到A文件窗口，命令模式，光标移到需复制起始行，输入复制的行数量，输入yy，进行复制
5. 按ctrl+w，按w，切换到B文件窗口；命令模式，光标移到需粘贴行，输入p，完成粘贴

[参考](https://www.cnblogs.com/ruichenduo/p/10772018.html)

### 多行复制

**命令模式下**，将第9行至第15行的数据，复制到第16行

`：9，15 copy 16` 或 `：9，15 co 16`
由此可有：
`：9，15 move 16` 或` :9,15 m 16` 将第9行到第15行的文本内容到第16行的后面 

[参考](https://www.cnblogs.com/MMLoveMeMM/articles/3707287.html)

## 多窗口显示

1. 使用 vim 先打开第一个文件，接着输入命 令 `:sp要打开的第二个文件的绝对路径`水平切分窗口，然后按回车键；如果想垂直切分窗口则可以输入 `:vsp要打开的第二个文件的绝对路径`;
2. 也可以直接执行命令`vim -o 第一个文件名的绝对路径 第二个文件名的绝对路径`。

[参考](https://blog.csdn.net/dyausasd/article/details/93394984)

## 注释

命令模式下

1. 在 10 - 20 行添加 // 注释 `:10,20s#^#//#g`
2. 在 10 - 20 行删除 // 注释 `:10,20s#^//##g`

## 缩进

命令模式下

1. 在10 - 20行缩进一个tab `:10,20>`
2. 在10 - 20行缩回一个tab `:10,20<`

## 替换
`:s` 命令来替换字符串。
`:s/well/good/` 替换当前行第一个 well 为 good
`:s/well/good/g` 替换当前行所有 well 为 good
`:n,$s/well/good/` 替换第 n 行开始到最后一行中每一行的第一个 well 为 good
`:n,$s/well/good/g` 替换第 n 行开始到最后一行中每一行所有 well 为 good
n 为数字，若 n 为 .，表示从当前行开始到最后一行
`:%s/well/good/`（等同于 :g/well/s//good/） 替换每一行的第一个 well 为 good
`:%s/well/good/g`（等同于 :g/well/s//good/g） 替换每一行中所有 well 为 good
可以使用 # 作为分隔符，此时中间出现的 / 不会作为分隔符
`:s#well/#good/#` 替换当前行第一个 well/ 为 good/
`:%s#/usr/bin#/bin#g` 可以把文件中所有路径/usr/bin换成/bin

[参考](https://www.cnblogs.com/nkwy2012/p/6365714.html)
[生成txt脚本](https://www.jb51.net/article/142119.htm)

## 配置

在目录/etc/vim/下面，会有名为vimrc的文件，这是系统公共的vim配置文件，对**所有的用户**都是有效的。 如果只是希望对本用户有效，也可以在当前用户的家目录(~)下建立.vimrc文件

```shell
set autoindent           # 自动缩进
set smartindent          # 为C语言提供自动缩进
set number               # 显示行号
set langmenu=zh_CN.UTF-8
set helplang=cn          # 语言设置
set tabstop=4            # Tab键的宽度
set softtabstop=4        # 统一缩进为4
set wildmenu             # 命令补全
set showcmd              # 显示指令
set wrap	             # 自动换行
```

```shell
"进行版权声明的设置
"添加或更新头
autocmd BufNewFile *.cpp,*.c,*.h exec ":call TitleComment()"
"map <F5> :call TitleComment()<cr>'s
"add comment for C
function AddTitleForC()
    call append(0,"/*--------------------------------------------------------")
    call append(1,"* Author             :Jiaq.yang")
    call append(2,"* Email              :thinklook1@outlook.com")
    call append(3,"* Create time        :".strftime("%Y-%m-%d %H:%M"))
    call append(4,"* Last modified      :".strftime("%Y-%m-%d %H:%M"))
    call append(5,"* Filename           :".expand("%:t"))
    call append(6,"* Description        :")
    call append(7,"----------------------------------------------------------*/")
	call append(8,"#include <stdio.h>")
    echohl WarningMsg | echo "Successful in adding the copyright." | echohl None
endf
function AddTitleForCpp()
    call append(0,"/*--------------------------------------------------------")
    call append(1,"* Author             :Jiaq.yang")
    call append(2,"* Email              :thinklook1@outlook.com")
    call append(3,"* Create time        :".strftime("%Y-%m-%d %H:%M"))
    call append(4,"* Last modified      :".strftime("%Y-%m-%d %H:%M"))
    call append(5,"* Filename           :".expand("%:t"))
    call append(6,"* Description        :")
    call append(7,"----------------------------------------------------------*/")
	call append(8,"#include <iostream>")
	call append(9,"using namespace std;")
    echohl WarningMsg | echo "Successful in adding the copyright." | echohl None
endf
function AddTitleForh()
	let basename = expand("%:t:r")
	let includeGuard = '_'.toupper(basename).'_H_'
    call append(0,"/*--------------------------------------------------------")
    call append(1,"* Author             :Jiaq.yang")
    call append(2,"* Email              :thinklook1@outlook.com")
    call append(3,"* Create time        :".strftime("%Y-%m-%d %H:%M"))
    call append(4,"* Last modified      :".strftime("%Y-%m-%d %H:%M"))
    call append(5,"* Filename           :".expand("%:t"))
    call append(6,"* Description        :")
    call append(7,"----------------------------------------------------------*/")
	call append(8, "#ifndef ".includeGuard)
	call append(9, "#define ".includeGuard)
	call append(10,"")
	call append(11,"#endif ")
    echohl WarningMsg | echo "Successful in adding the copyright." | echohl None
endf
"更新最近修改时间和文件名
function UpdateTitle()
    normal m'
    execute '/# *Last modified:/s@:.*$@\=strftime(":\t%Y-%m-%d %H:%M")@'
    normal ''
    normal mk
    execute '/# *Filename:/s@:.*$@\=":\t\t".expand("%:t")@'
    execute "noh"
    normal 'k
    echohl WarningMsg | echo "Successful in updating the copyright." | echohl None
endfunction
"判断前10行代码里面，是否有Last modified这个单词，
"如果没有的话，代表没有添加过作者信息，需要新添加；
"如果有的话，那么只需要更新即可
function TitleComment()
    let n=1
    "默认为添加
    while n < 10
        let line = getline(n)
        if line =~ '^\#\s*\S*Last\smodified:\S*.*$'
            call UpdateTitle()
            return
        endif
        let n = n + 1
    endwhile
"	if &filetype == 'c' 
"		call AddTitleForC()
"	elseif &filetype == 'cpp'
"		call AddTitleForCpp()
"	endif
	if expand("%:e") == 'h'
		call AddTitleForh()
	elseif expand("%:e") == 'cpp'
		call AddTitleForCpp()
	elseif expand("%:e") == 'c'
	    call AddTitleForC()
	endif
endfunction
"自动补全
:inoremap ( ()<ESC>i
":inoremap ) <c-r>=ClosePair(')')<CR>
:inoremap { {<CR>}<ESC>O
":inoremap } <c-r>=ClosePair('}')<CR>
:inoremap [ []<ESC>i
":inoremap ] <c-r>=ClosePair(']')<CR>
:inoremap " ""<ESC>i
:inoremap ' ''<ESC>i

set tabstop=4
set softtabstop=4
set shiftwidth=4
set number
set helplang=cn
set smartindent
set wildmenu
set showcmd
set wrap
set completeopt=preview,menu
set autowrite
"打开文件类型检测, 加了这句才可以用智能补全
set completeopt=longest,menu
set syntax=on
```

[参考1]:https://www.cnblogs.com/zlhao/archive/2012/02/01/2335081.html	"vim配置"
[参考2]:https://www.cnblogs.com/mfryf/p/3643349.html	"vim一键添加注释"
[参考3]: https://blog.51cto.com/thedream/1873060	"vim个性化设置"

[参考4]: https://www.cnblogs.com/ma6174/archive/2011/12/10/2283393.html	"vim自动配置"
[参考5]: https://www.cnblogs.com/baisheng/p/13915937.html	"vim header文件"