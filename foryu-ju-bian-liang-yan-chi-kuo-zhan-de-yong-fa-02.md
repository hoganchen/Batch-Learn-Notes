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

```
@echo off
setlocal enabledelayedexpansion

rem https://www.cnblogs.com/ini_always/archive/2012/02/16/2355031.html
rem http://www.bathome.net/thread-43675-1-1.html

set count=100
set HOUR=%time: =0%

for /l %%j in (1 1 %count%) do (
    echo Start to run pts test...
    PTSControlClient.exe gap_debug.xml COM28 0 > pts_test_%date:~0,4%%date:~5,2%%date:~8,2%%HOUR:~0,2%%time:~3,2%%time:~6,2%.log 2>&1

    move /Y Logs\GAP_CONN_GCEP_BV-01-C_test.log Logs\GAP_CONN_GCEP_BV-01-C_test_!date:~0,4!!date:~5,2!!date:~8,2!!HOUR:~0,2!!time:~3,2!!time:~6,2!.log
    move /Y Logs\GAP_CONN_GCEP_BV-01-C_pts.log Logs\GAP_CONN_GCEP_BV-01-C_pts_!date:~0,4!!date:~5,2!!date:~8,2!!HOUR:~0,2!!time:~3,2!!time:~6,2!.log

    taskkill /F /T /IM pts.exe
    taskkill /F /T /IM fts.exe
    taskkill /F /T /IM PTSControlClient.exe
)

pause
```

```
@echo off
setlocal enabledelayedexpansion

rem https://www.cnblogs.com/ini_always/archive/2012/02/16/2355031.html
rem http://www.bathome.net/thread-43675-1-1.html

set count=100
set HOUR=%time: =0%

for /l %%j in (1 1 %count%) do (
    echo Start to run pts test...
    rem 使用延时变量赋值的变量，在使用时需要以"!variable!"方式引用
    set curtime=!date:~0,4!!date:~5,2!!date:~8,2!!HOUR:~0,2!!time:~3,2!!time:~6,2!

    PTSControlClient.exe gap_debug.xml COM28 0 > pts_test_!curtime!.log 2>&1

    cd Logs

    echo start to rename test log...
    rem for循环中匹配多个后缀名
    for %%i in (*_pts.log, *_test.log) do (
        move %%i %%~ni_!curtime!%%~xi > nul 2>&1
    )

    cd ..

    echo start to terminal the pts process...
    taskkill /F /T /IM pts.exe > nul 2>&1
    taskkill /F /T /IM fts.exe > nul 2>&1
    taskkill /F /T /IM PTSControlClient.exe > nul 2>&1
)

pause

```

```
@echo off
REM 开启延时变量
setlocal enabledelayedexpansion
REM 关闭延时变量
REM setlocal disabledelayedexpansion

REM set PATH=%PATH%;C:\Anaconda3;C:\ProgramData\Anaconda3
set PATH=%PATH%;.\venv\Scripts

for /L %%i in (1,1,10) do (
    REM 延时变量需要使用!var!的方式使用

    REM 将空格替换为0，因为如果小时少于10点，小时数字的第一个字符为空格，所以将空格替换为0
    set HOURS=!time: =0!

    REM 字符串截取，针对第一个截取表达式，含义为从第0个字符开始，截取4个字符
    set datestr=!date:~0,4!!date:~5,2!!date:~8,2!!HOURS:~0,2!!time:~3,2!!time:~6,2!
    REM echo !datestr!
    REM ping 127.0.0.1 -n 2 > nul

    pyinstaller --clean -F -w -c map_parser.py
    copy /y dist\map_parser.exe .\map_parser_!datestr!.exe
)

REM python map_parser.py -s D:\BALBOA_SW_CODE\00_SW\00_SW_DEV\app -d true -f true -r true > map_parser_%date:~0,4%%date:~5,2%%date:~8,2%%HOUR:~0,2%%time:~3,2%%time:~6,2%.log 2>&1

pause
```
