### For语句变量延迟扩展的用法02

```
@echo off
setlocal EnableDelayedExpansion
set PATH=%PATH%;C:\Keil_v5\UV4;C:\Keil_v5\ARM\ARMCC\Bin;

set curpwd=%cd%

cd /d %curpwd%
:: cd /d ..\..\new_app\projects\ble\ble_peripheral
cd /d ..\..\new_app\projects\test\peripheral_test_prj\pwm_test\pwm_hal_test

for /f %%i in ('dir *.uvprojx /s /b') do (
    cd /d %%~dpi

    for /f "delims=<> tokens=3" %%k in ('findstr "<TargetName>" %%~nxi') do (
        echo %%~dpi

        echo %%i | findstr /i "Keil_5_sym" > nul
        if errorlevel 1 (
            set keiltype=KEIL5
        ) else (
            set keiltype=KEIL5-SYM
        )

        set target=%%k
        set target=!target:_=-!

        set project=%%~ni
        set project=!project:_=-!

        echo Command: "UV4 -j0 -r %%~nxi -t %%k -o %curpwd%\build_logs\peripheral_!keiltype!_%%~ni_!target!.log"
        echo Command: "UV4 -j0 -r %%~nxi -t %%k -o %curpwd%\build_logs\peripheral_!keiltype!_!project!_%%k.log"
    )
)

pause
```



