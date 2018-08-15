### For语句变量扩展的用法01

```
@echo off
echo ---显示"dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah"
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 不扩展变量 %%i
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~fI %%~fi --扩充到一个完全合格的路径名
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~dI %%~di --仅将变量扩充到一个驱动器号
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~pI %%~pi --仅将变量扩充到一个路径
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~nI %%~ni --仅将变量扩充到一个文件名
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~xI %%~xi --仅将变量扩充到一个文件扩展名
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~sI %%~si --扩充的路径只含有短名
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~aI %%~ai --将变量扩充到文件的文件属性
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~tI %%~ti --将变量扩充到文件的日期/时间
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~zI %%~zi --将变量扩充到文件的大小
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~$PATH:I %%~$PATH:i --查找列在路径环境变量的目录，并将变量扩充到找到的第一个完全合格的名称
echo ---以下显示组合修饰符来得到多重结果---：
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~dpI %%~dpi --仅将变量扩充到一个驱动器号和路径
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~nxI %%~nxi --仅将变量扩充到一个文件名和扩展名
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~fsI %%~fsi --仅将变量扩充到一个带有短名的完整路径名
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~dp$PATH:I %%~dp$PATH:i --查找列在路径环境变量的目录，并将变量扩充到找到的第一个驱动器号和路径
for /f "delims==" %%i in ('dir %HOMEDRIVE%%HOMEPATH%\desktop\desktop.ini /b /ah') do echo 扩展变量到~ftzaI %%~ftzai --将变量扩充到类似输出线路的DIR
echo.
echo ---显示"dir C:\WINDOWS\system32\notepad.exe /b"
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 不扩展变量 %%i
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~fI %%~fi --扩充到一个完全合格的路径名
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~dI %%~di --仅将变量扩充到一个驱动器号
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~pI %%~pi --仅将变量扩充到一个路径
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~nI %%~ni --仅将变量扩充到一个文件名
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~xI %%~xi --仅将变量扩充到一个文件扩展名
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~sI %%~si --扩充的路径只含有短名
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~aI %%~ai --将变量扩充到文件的文件属性
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~tI %%~ti --将变量扩充到文件的日期/时间
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~zI %%~zi --将变量扩充到文件的大小
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~$PATH:I %%~$PATH:i --查找列在路径环境变量的目录，并将变量扩充到找到的第一个完全合格的名称
echo ---以下显示组合修饰符来得到多重结果---：
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~dpI %%~dpi --仅将变量扩充到一个驱动器号和路径
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~nxI %%~nxi --仅将变量扩充到一个文件名和扩展名
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~fsI %%~fsI --仅将变量扩充到一个带有短名的完整路径名
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~dp$PATH:I %%~dp$PATH:i --查找列在路径环境变量的目录，并将变量扩充到找到的第一个驱动器号和路径
for /f "delims==" %%i in ('dir C:\WINDOWS\system32\notepad.exe /b') do echo 扩展变量到~ftzaI %%~ftzai --将变量扩充到类似输出线路的DIR
Pause
```

**注意输出结果中，第二次for循环变量扩展中的变量还是用的第一次for循环的变量，待确认原因**

输出如下:

```

C:\Users\hoganchen\Desktop>for_extended.bat
---显示"dir C:\Users\hoganchen\desktop\desktop.ini /b /ah"
不扩展变量 desktop.ini
扩展变量到~fI C:\Users\hoganchen\Desktop\desktop.ini --扩充到一个完全合格的路径名
扩展变量到~dI C: --仅将变量扩充到一个驱动器号
扩展变量到~pI \Users\hoganchen\Desktop\ --仅将变量扩充到一个路径
扩展变量到~nI desktop --仅将变量扩充到一个文件名
扩展变量到~xI .ini --仅将变量扩充到一个文件扩展名
扩展变量到~sI C:\Users\CHENLI~1\Desktop\desktop.ini --扩充的路径只含有短名
扩展变量到~aI --ahs---- --将变量扩充到文件的文件属性
扩展变量到~tI 2017/09/19 09:09 --将变量扩充到文件的日期/时间
扩展变量到~zI 282 --将变量扩充到文件的大小
扩展变量到~$PATH:I C:\Windows\System32\desktop.ini --查找列在路径环境变量的目录，并将变量扩充到找到的第一个完全合格的名称
---以下显示组合修饰符来得到多重结果---：
扩展变量到~dpI C:\Users\hoganchen\Desktop\ --仅将变量扩充到一个驱动器号和路径
扩展变量到~nxI desktop.ini --仅将变量扩充到一个文件名和扩展名
扩展变量到~fsI C:\Users\CHENLI~1\Desktop\desktop.ini --仅将变量扩充到一个带有短名的完整路径名
扩展变量到~dp$PATH:I C:\Windows\System32\ --查找列在路径环境变量的目录，并将变量扩充到找到的第一个驱动器号和路径
扩展变量到~ftzaI --ahs---- 2017/09/19 09:09 282 C:\Users\hoganchen\Desktop\desktop.ini --将变量扩充到类似输出线路的DIR

---显示"dir C:\WINDOWS\system32\notepad.exe /b"
不扩展变量 notepad.exe
扩展变量到~fI C:\Users\hoganchen\Desktop\notepad.exe --扩充到一个完全合格的路径名
扩展变量到~dI C: --仅将变量扩充到一个驱动器号
扩展变量到~pI \Users\hoganchen\Desktop\ --仅将变量扩充到一个路径
扩展变量到~nI notepad --仅将变量扩充到一个文件名
扩展变量到~xI .exe --仅将变量扩充到一个文件扩展名
扩展变量到~sI C:\Users\CHENLI~1\Desktop\notepad.exe --扩充的路径只含有短名
扩展变量到~aI  --将变量扩充到文件的文件属性
扩展变量到~tI  --将变量扩充到文件的日期/时间
扩展变量到~zI  --将变量扩充到文件的大小
扩展变量到~$PATH:I C:\Windows\System32\notepad.exe --查找列在路径环境变量的目录，并将变量扩充到找到的第一个完全合格的名称
---以下显示组合修饰符来得到多重结果---：
扩展变量到~dpI C:\Users\hoganchen\Desktop\ --仅将变量扩充到一个驱动器号和路径
扩展变量到~nxI notepad.exe --仅将变量扩充到一个文件名和扩展名
扩展变量到~fsI %~fsI --仅将变量扩充到一个带有短名的完整路径名
扩展变量到~dp$PATH:I C:\Windows\System32\ --查找列在路径环境变量的目录，并将变量扩充到找到的第一个驱动器号和路径
扩展变量到~ftzaI C:\Users\hoganchen\Desktop\notepad.exe --将变量扩充到类似输出线路的DIR
请按任意键继续. . .
```



