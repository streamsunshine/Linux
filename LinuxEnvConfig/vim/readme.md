# vim

.vim.tar.bz2是个人目录下的.vim的打包文件（这个貌似没有什么作用）

.vimrc是配置文件

配置文件的使用方法，将文件下载到你的个人目录下（~），如果是通过window下载的可能提示

```
E492: Not an editor command: ^M
```

进入 .vimrc 后，运行

```
:set fileformat=unix
```

即可解决这个问题。



如果使用的vim存在乱码，在 .vimrc中添加下面的指令

```
set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936
set termencoding=utf-8
set encoding=utf-8
```

