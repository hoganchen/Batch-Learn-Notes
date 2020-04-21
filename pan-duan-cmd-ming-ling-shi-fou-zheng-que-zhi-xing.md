### 判断CMD命令是否正确执行

```
:@echo off

set PATH:%PATH%;C:\Anaconda3;C:\ProgramData\Anaconda3

python --version

dir *.py

if %errorlevel% equ 0 (
    echo error not happening...
) else (
    echo error happening...
)
```



