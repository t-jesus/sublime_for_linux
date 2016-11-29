##Fedora 24 安装搜狗输入法、解决sublime在Linux下无法输入中文
###1、添加 Fedora 中文社区软件源
* dnf config-manager --add-repo=http://repo.fdzh.org/FZUG/FZUG.repo

###2、安装搜狗输入法
* sudo dnf install sogoupinyin -y

###3、配置搜狗输入法
* 略

###4、新建sublime_imfix.c
* 内容略

###5、安装gt
* dnf install libgnomeui-devel -y（如果是ubuntu的话 sudo apt-get install build-essential libgtk2.0-dev）

###6、编译
* gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC

###7、拷贝文件到sublime的根目录下
* libsublime-imfix.so

###8、测试
* bash -c 'LD_PRELOAD=sublime安装目录/libsublime-imfix.so sublime安装目录/sublime_text' %F

###9、修改/usr/share/applications/sublime.desktop
    [Desktop Entry]
    Type=Application
    Encoding=UTF-8
	Name=Sublime-text3
	Comment=sublime-text3
	Exec=bash -c 'LD_PRELOAD=sublime安装目录/libsublime-imfix.so sublime安装目录/sublime_text' -n
	Icon=sublime安装目录/Icon/128x128/sublime-text.png
	Terminal=false
	StartupNotify=false

###10、问题
* 虽然可以输入中文，但是还是有点小问题是：输入时输入法不跟随光标，但是现在可以使用搜狗输入法且可以在sublime下使用搜狗输入法，如果有哪位兄弟解决了分享下
