### 清空Temp文件夹

* ##### 清除临时文件夹01

```
@echo off

set pwd=%cd%
set type=tmp

:: cd /d %TEMP%
cd /d %USERPROFILE%\AppData\Local\Temp

for /f %%i in ('dir /b *.tmp^|find /v /c ""') do set new_count=%%i
echo total have %new_count% %type% files

del /s /q *.tmp
:: del /s /q *.tmp 1>nul 2>nul

for /f %%j in ('dir /b') do (
    echo %%j

    if exist %%j\ (rmdir /s /q %%j) else (del /s /q %%j)
)

cd /d %pwd%

pause
```

* ##### 清除临时文件夹02

```
@echo off

set pwd=%cd%
set type=tmp

:: cd /d %TEMP%
cd /d %USERPROFILE%\AppData\Local\Temp

:: https://my.oschina.net/solee/blog/75763
:: 统计特定文件夹下的文件个数的DOS命令：dir /s /b | find /c ":"，或者：dir /s /b | find /v /c ""
:: dir /b *.tmp^ | find /v /n ""
:: dir /b *.tmp^ | find /v /c ""
:: dir /b ^ | findstr /n .*.tmp

:: https://zhidao.baidu.com/question/344424350.html
for /f "delims=:" %%i in ('dir /b *.%type%^|findstr /n .') do set count=%%i

:: https://www.zhihu.com/question/51968876
:: for /f "tokens=1* delims=:" %%i in ('dir /a-d /b *.%type%^|findstr /n /r "$"') do @set count=%%i

echo total have %count% %type% files

for /f %%i in ('dir /b *.tmp^|find /v /c ""') do set new_count=%%i
echo total have %new_count% %type% files

del /s /q *.tmp

cd /d %pwd%

pause
```

* ##### IF用法

```
if exist build_logs (
    del /s /q build_logs
)
```



