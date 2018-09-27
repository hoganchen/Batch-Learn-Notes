### del命令不回显

```
@echo off

del /f /s /q test_report\*
:: del /f /s /q test_report\* > nul 2> nul

for /f %%i in ('dir *.xml *.html /b') do (
    type %%i > test_report\%%i
)

```



