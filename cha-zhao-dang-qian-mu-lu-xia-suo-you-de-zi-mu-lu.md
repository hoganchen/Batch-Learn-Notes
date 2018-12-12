### 查找当前目录下所有的子目录

```
@echo off
: setlocal EnableDelayedExpansion

set curpwd=%cd%

for /f %%i in ('dir /A:D /B *workspace') do (
    echo i: %%i
    echo dpi: %%~dpi
    echo dpni: %%~dpni
    
    for /f %%j in ('dir /A:D /B %%i') do (
        echo folder j is: %%j
        echo folder dpj is: %%~dpj
        echo folder dpnj is: %%~dpnj
        echo folder pathj is: %%~dpni\%%j
    )
)

pause
```



