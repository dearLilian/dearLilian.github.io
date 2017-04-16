---
layout: post
title: linux下的sublime安装与配置
date: 2017-04-15
tag: linux
---

目录

* TOC 
{:toc}


## sublime的安装与配置

### 安装sublime text 3

> 下载地址：https://download.sublimetext.com/sublime-text_build-3126_amd64.deb

将下载好的文件放在```/home/Downloads/```文件夹下。

安装方法：


- ```ctrl+alt+T```打开终端
- 进入```/home/Downloads/```
```shell
cd /home/Downloads
```
- 安装sublime
```shell
sudo dpkg -i  sublime-text_build-3126_amd64.deb
```

### 配置sublime Package Control

有两种安装方式：

 1. 命令方式

首先打开sublime，然后按```ctrl+ ~```。此时会打开sublime的命令输入栏。

对于sublime3的话，在该栏中输入：

```python
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

然后回车等待命令执行结束。


在linux下配置有时候会出现一些奇葩的bug。反正就是安装不成功。那就采用下面这种。


 2. 手动安装

浏览器，打开网址```https://github.com/wbond/package_control```

然后打包下载。

或者直接在下载器中输入下载链接```https://codeload.github.com/wbond/package_control/zip/master``下载即可。


然后将该下载的文件放在sublime下的Installed Packages文件夹下，并重命名为Package Control.sublime-package即可。重启sublime。


### 配置sublime中文输入

- 首先假定已经安装好fcix以及搜狗输入法等中文输入法了。

- 然后打开sublime，点击```Preference```-> ```Browse Packages...```

- 然后回到该目录的上级目录，即```sublime-text-3```

- 右击鼠标，点击```open in terminal```

- 然后，创建文件```sublime_imfix.c```。

```shell
gedit sublime_imfix.c
```

- 在该新建文件中输入代码：

```c
/*
 * sublime-imfix.c
 * Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
 * By Cjacker Huang <jianzhong.huang at i-soft.com.cn> *
 *
 * gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
 * LD_PRELOAD=./libsublime-imfix.so sublime_text
 */
#include <gtk/gtk.h>
#include <gdk/gdkx.h>

typedef GdkSegment GdkRegionBox;

struct _GdkRegion
{
    long size;
    long numRects;
    GdkRegionBox *rects;
    GdkRegionBox extents;
};

GtkIMContext *local_context;

void
gdk_region_get_clipbox (const GdkRegion *region,
                        GdkRectangle    *rectangle)
{
    g_return_if_fail (region != NULL);
    g_return_if_fail (rectangle != NULL);

    rectangle->x = region->extents.x1;
    rectangle->y = region->extents.y1;
    rectangle->width = region->extents.x2 - region->extents.x1;
    rectangle->height = region->extents.y2 - region->extents.y1;
    GdkRectangle rect;
    rect.x = rectangle->x;
    rect.y = rectangle->y;
    rect.width = 0;
    rect.height = rectangle->height;

    //The caret width is 2;
    //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
    if (rectangle->width == 2 && GTK_IS_IM_CONTEXT(local_context)) {
        gtk_im_context_set_cursor_location(local_context, rectangle);
    }
}

//this is needed, for example, if you input something in file dialog and return back the edit area
//context will lost, so here we set it again.

static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
{
    XEvent *xev = (XEvent *)xevent;

    if (xev->type == KeyRelease && GTK_IS_IM_CONTEXT(im_context)) {
        GdkWindow *win = g_object_get_data(G_OBJECT(im_context), "window");

        if (GDK_IS_WINDOW(win)) {
            gtk_im_context_set_client_window(im_context, win);
        }
    }

    return GDK_FILTER_CONTINUE;
}

void gtk_im_context_set_client_window (GtkIMContext *context,
                                       GdkWindow    *window)
{
    GtkIMContextClass *klass;
    g_return_if_fail (GTK_IS_IM_CONTEXT (context));
    klass = GTK_IM_CONTEXT_GET_CLASS (context);

    if (klass->set_client_window) {
        klass->set_client_window (context, window);
    }

    if (!GDK_IS_WINDOW (window)) {
        return;
    }

    g_object_set_data(G_OBJECT(context), "window", window);
    int width = gdk_window_get_width(window);
    int height = gdk_window_get_height(window);

    if (width != 0 && height != 0) {
        gtk_im_context_focus_in(context);
        local_context = context;
    }

    gdk_window_add_filter (window, event_filter, context);
}
```

保存关闭。

- 然后进入在终端进入该目录```/home/wenbao/.config/sublime-text-3```，这里```wenbao```是用户名。

```shell
cd /home/wenbao/.config/sublime-text-3
```

- 编译成共享库

```shell
gcc -shared -o libsublime-imfix.so sublime-imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
```

在执行以上命令时候可能会提示缺少包，可以通过如下命令安装所需要的包即可

命令如下：

```shell
sudo apt-get install gtk+-2.0
```

以上命令即为安装所缺少编译时需要的的包，执行完以上命令之后，重复执行编译命令即可通过

```shell
gcc -shared -o libsublime-imfix.so sublime-imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
```
然后就可以正常编译了。此时，当前目录下产生了共享库```libsublime-imfix.so```这个文件。

- 移动 libsublime-imfix.so 至 /usr/lib/

命令如下：

```shell
mv libsublime-imfix.so /usr/lib
```
- 为了使得该共享库生效，需要修改sublime-text的启动命令。

- 打开终端进入目录```/usr/share/applicaitons```

命令为：

```shell
cd /usr/share/applications
```

- 使用gedit打开并修改sublime-text.desktop

命令：

```shell
sudo gedit sublime-text.desktop
```

找到三个

```Exec=/opt/sublime_text/sublime_text' %F```

在```Exec=```后添加```bash -c 'LD_PRELOAD=/usr/lib/libsublime-imfix.so ```

保存退出即可。

- 最后，重启sublime。可以发现已经能输入中文了。


### 配置sublime的markdown插件

由于网络问题还是啥的，插件无法使用Package Control来安装。只能手动安装。


安装方法就是去github下载插件源码zip文件，然后将文件后缀名改为```sublime-package```，然后放在```/home/.config/sublime-text-3/Installed Packages/```下即可。


Note: 经过一系列折腾，我还是被它深深的打败了，最后决定弃坑。不再执着于sublime+markdown。


于是，在网上搜索了另外一个markdown编辑器，即Remarkable，直接点击链接```https://remarkableapp.github.io/files/remarkable_1.87_all.deb```下载deb文件，双击安装即可。

### 配置sublime上的java开发环境
这里可能遇到一个小问题，当Browse Packages失效时候，找不到上面两个目录时，需要使用命令行来操作。

对于有空格的文件路径，空格要使用```\+空格```。例如：进入目录```home/wenbao/.config/sublime-text-3/Installed Packages```

命令为：

```shell
cd /home/wenbao/.config/sublime-text-3/Installed\ Packages
```
