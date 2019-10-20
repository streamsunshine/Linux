# tmux

.tmux.tar.bz2是个人目录下的.tmux的打包文件

.tmuxrc是tmux件

## ISSUE

&emsp;在使用tmux和xshell的时候，可能导致在xshell的窗口选择文本时，无法选择的问题。这是因为tmux设置了鼠标功能，在窗口使用鼠标选择文本时，鼠标操作被tmux读取，从而xshell的无效。可以通过在.tmux.conf中搜索mouse，注释掉tmux中鼠标相关的设置即可。修改之后可以在xshell窗口进行选择文本，复制粘贴。

配置完以后，重启tmux起效，或者先按C+b，然后输入：，进入命令行模式， 在命令行模式下输入：

source-file ~/.tmux.conf
