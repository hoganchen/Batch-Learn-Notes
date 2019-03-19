### 清空Temp文件夹

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

```
if exist build_logs (
    del /s /q build_logs
)
```



