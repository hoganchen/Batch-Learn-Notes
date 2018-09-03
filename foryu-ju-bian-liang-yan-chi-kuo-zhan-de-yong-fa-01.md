### For语句变量延迟扩展的用法01

```
: setlocal enabledelayedexpansion用于开启变量延迟，这是告诉解释器，在遇到复合语句的时候，不要将其作为一条语句同时处理，
: 而仍然一条一条地去解释。但是这时必须用!str!来引用变量，如果仍然用%str%引用是不起作用的。

@echo off
setlocal EnableDelayedExpansion
set PATH=%PATH%;C:\Keil_v5\UV4;C:\Keil_v5\ARM\ARMCC\Bin;

set curpwd=%cd%

cd /d %curpwd%
cd /d ..\..\new_app\projects\ble\ble_peripheral

for /f %%i in ('dir *.uvprojx /s /b') do (
    cd /d %%~dpi

    for /f "delims=<> tokens=3" %%k in ('findstr "<TargetName>" %%~nxi') do (
        echo %%~dpi

        echo %%i | findstr /i "Keil_5_sym" > nul
        if errorlevel 1 (
            set keiltype=KEIL5
            echo not found
        ) else (
            set keiltype=KEIL5-SYM
            echo found
        )

        echo Command: "UV4 -j0 -r %%~nxi -t %%k -o %curpwd%\build_logs\peripheral_!keiltype!_%%~ni.log"
    )
)

pause
```



