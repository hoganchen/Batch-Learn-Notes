# Windows下删除大量文件的快速方法

[http://blchen.com/fareast-way-to-delete-a-folder-contains-large-number-of-files-in-windows/](http://blchen.com/fareast-way-to-delete-a-folder-contains-large-number-of-files-in-windows/)

在Windows下删除文件夹有很多方法，比如拖到回收站，Shift+Del直接跳过回收站删除，命令行方式下用rs /s/q，等等等等。但是如果要删除的是一个包含巨多文件的文件夹，那上面这几个方式就不够好用了。直接删除文件夹，Windows就会先傻傻先浪费几个小时计算这个文件夹的大小，然后才提示你时候删除。

下面是我测试出的最快的删除大文件夹的方法

```
del /f/s/q dirname > nul
rmdir /s/q dirname


C:\projects>del /?
删除一个或数个文件。

DEL [/P] [/F] [/S] [/Q] [/A[[:]attributes]] names
ERASE [/P] [/F] [/S] [/Q] [/A[[:]attributes]] names

  names         指定一个或多个文件或者目录列表。
                通配符可用来删除多个文件。
                如果指定了一个目录，该目录中的所
                有文件都会被删除。

  /P            删除每一个文件之前提示确认。
  /F            强制删除只读文件。
  /S            删除所有子目录中的指定的文件。
  /Q            安静模式。删除全局通配符时，不要求确认
  /A            根据属性选择要删除的文件
  属性          R  只读文件                     S  系统文件
                H  隐藏文件                     A  存档文件
                I  无内容索引文件               L  重分析点
                -  表示“否”的前缀

如果命令扩展被启用，DEL 和 ERASE 更改如下:

/S 开关的显示句法会颠倒，即只显示已经
删除的文件，而不显示找不到的文件。


C:\projects>rmdir /?
删除一个目录。

RMDIR [/S] [/Q] [drive:]path
RD [/S] [/Q] [drive:]path

    /S      除目录本身外，还将删除指定目录下的所有子目录和
            文件。用于删除目录树。

    /Q      安静模式，带 /S 删除目录树时不要求确认
```

究竟多块？测试下来，对于大小在几十G，包含数十万小文件的文件夹，耗时大概是rd /s/q的一半。

**推荐使用rmdir，比del效率更高。**

