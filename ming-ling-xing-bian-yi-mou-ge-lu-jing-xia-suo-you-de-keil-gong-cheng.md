### 命令行编译某个路径下所有的Keil工程

```
@echo off
set PATH=%PATH%;C:\Keil_v5\UV4;C:\Keil_v5\ARM\ARMCC\Bin;

if not exist build_log (
    mkdir build_log
) else (
    del /s /q build_log
)

set curpwd=%cd%
cd /d %1

for /f %%i in ('dir /s /b *.uvprojx^|find /v /c ""') do set project_count=%%i

for /f %%i in ('dir *.uvprojx /s /b') do (
        cd /d %%~dpi
        
        echo Current Path: %%~dpi
        echo Project Name: %%~nxi

        for /f "delims=<> tokens=3" %%k in ('findstr "<TargetName>" %%~nxi') do (
            echo Command: "UV4 -j0 -r %%~nxi -t %%k -o %curpwd%\build_log\%%~ni.txt"

            UV4 -j0 -r %%~nxi -t %%k -o %curpwd%\build_log\%%~ni.txt
            type %curpwd%\build_log\%%~ni.txt
        )
)

cd /d %curpwd%

for /f %%i in ('dir /b build_log\*.txt^|find /v /c ""') do set compile_count=%%i

echo;
echo;
echo ################################################################################
echo Total project number: %project_count%, total compile project number: %compile_count%
echo ################################################################################

for /f %%i in ('dir build_log\*.txt /s /b') do (
    echo;
    echo;
    echo ################################################################################
    echo For %%~ni project, build result: 
    echo ################################################################################
    findstr "Warning(s)" %%i
    findstr "Elapsed" %%i
)

pause
```



