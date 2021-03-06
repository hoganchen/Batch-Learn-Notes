### Batch常用命令

* #### 删除文件夹

```
del /s /q XXX_Test
rmdir /s /q XXX_Test

C:\Users\xxx>del /?
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

C:\Users\xxx>rmdir /?
删除一个目录。

RMDIR [/S] [/Q] [drive:]path
RD [/S] [/Q] [drive:]path

    /S      除目录本身外，还将删除指定目录下的所有子目录和
            文件。用于删除目录树。

    /Q      安静模式，带 /S 删除目录树时不要求确认

```

* #### 复制文件夹

```
xcopy E:\XXX XXX_Test /s /e /h

C:\Users\xxx>xcopy /?
复制文件和目录树。

XCOPY source [destination] [/A | /M] [/D[:date]] [/P] [/S [/E]] [/V] [/W]
                           [/C] [/I] [/Q] [/F] [/L] [/G] [/H] [/R] [/T] [/U]
                           [/K] [/N] [/O] [/X] [/Y] [/-Y] [/Z] [/B]
                           [/EXCLUDE:file1[+file2][+file3]...]

  source       指定要复制的文件。
  destination  指定新文件的位置和/或名称。
  /A           仅复制有存档属性集的文件，但不更改属性。
  /M           仅复制有存档属性集的文件，并关闭存档属性。
  /D:m-d-y     复制在指定日期或指定日期以后更改的文件。
               如果没有提供日期，只复制那些源时间比目标时间新的文件。
  /EXCLUDE:file1[+file2][+file3]...
               指定含有字符串的文件列表。每个字符串在文件中应位于单独的一行。
               如果任何字符串与复制文件的绝对路径的任何部分相符，则排除复制
               该文件。例如，指定如 \obj\ 或 .obj 的字符串会分别排除目录
               obj 下面的所有文件或带有 .obj 扩展名的所有文件。
  /P           创建每个目标文件之前提示您。
  /S           复制目录和子目录，不包括空目录。
  /E           复制目录和子目录，包括空目录。与 /S /E 相同。可以用来修改 /T。
  /V           验证每个新文件的大小。
  /W           提示您在复制前按键。
  /C           即使有错误，也继续复制。
  /I           如果目标不存在，且要复制多个文件，则假定目标必须是目录。
  /Q           复制时不显示文件名。
  /F           复制时显示完整的源文件名和目标文件名。
  /L           显示要复制的文件。
  /G           允许将加密文件复制到不支持加密的目标。
  /H           也复制隐藏文件和系统文件。
  /R           覆盖只读文件。
  /T           创建目录结构，但不复制文件。不包括空目录或子目录。/T /E 包括
               空目录和子目录。
  /U           只复制已经存在于目标中的文件。
  /K           复制属性。一般的 Xcopy 会重设只读属性。
  /N           用生成的短名称复制。
  /O           复制文件所有权和 ACL 信息。
  /X           复制文件审核设置(隐含 /O)。
  /Y           取消提示以确认要覆盖现有目标文件。
  /-Y          要提示以确认要覆盖现有目标文件。
  /Z           在可重新启动模式下复制网络文件。
  /B           复制符号链接本身与链接目标相对。
  /J           复制时不使用缓冲的 I/O。推荐复制大文件时使用。

开关 /Y 可以预先在 COPYCMD 环境变量中设置。
这可能被命令行上的 /-Y 覆盖。

```

* #### 复制文件

```
copy /y ..\xxx\xxx.c ..\..\..\xxx\yyy\zzz\

C:\Users\xxx>copy /?
将一份或多份文件复制到另一个位置。

COPY [/D] [/V] [/N] [/Y | /-Y] [/Z] [/L] [/A | /B ] source [/A | /B]
     [+ source [/A | /B] [+ ...]] [destination [/A | /B]]

  source       指定要复制的文件。
  /A           表示一个 ASCII 文本文件。
  /B           表示一个二进位文件。
  /D           允许解密要创建的目标文件
  destination  为新文件指定目录和/或文件名。
  /V           验证新文件写入是否正确。
  /N           复制带有非 8dot3 名称的文件时，
               尽可能使用短文件名。
  /Y           不使用确认是否要覆盖现有目标文件
               的提示。
  /-Y          使用确认是否要覆盖现有目标文件
               的提示。
  /Z           用可重新启动模式复制已联网的文件。
/L           如果源是符号链接，请将链接复制
               到目标而不是源链接指向的实际文件。

命令行开关 /Y 可以在 COPYCMD 环境变量中预先设定。
这可能会被命令行上的 /-Y 替代。除非 COPY
命令是在一个批处理脚本中执行的，默认值应为
在覆盖时进行提示。

要附加文件，请为目标指定一个文件，为源指定
数个文件(用通配符或 file1+file2+file3 格式)。

```

* #### 移动或重命名文件或和文件夹

```
move /y ..\..\..\xxx\build_bak ..\..\..\xxx\build

C:\Users\xxx>move /?
移动文件并重命名文件和目录。

要移动至少一个文件:
MOVE [/Y | /-Y] [drive:][path]filename1[,...] destination

要重命名一个目录:
MOVE [/Y | /-Y] [drive:][path]dirname1 dirname2

  [drive:][path]filename1 指定您想移动的文件位置和名称。
  destination             指定文件的新位置。目标可包含一个驱动器号
                          和冒号、一个目录名或组合。如果只移动一个文件
                          并在移动时将其重命名，您还可以包括文件名。
  [drive:][path]dirname1  指定要重命名的目录。
  dirname2                指定目录的新名称。

  /Y                      取消确认覆盖一个现有目标文件的提示。
  /-Y                     对确认覆盖一个现有目标文件发出提示。

命令行开关 /Y 可以出现在 COPYCMD 环境变量中。这可以用命令行上
的 /-Y 替代。默认值是，除非 MOVE 命令是从一个批脚本内
执行的，覆盖时都发出提示。
```



