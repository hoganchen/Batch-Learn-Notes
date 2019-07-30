### 计划任务之自动更新代码

```
@echo on

set LOG_PATH_NAME=D:\schedule_tasks\svn_update_%date:~0,4%%date:~5,2%%date:~8,2%%time:~0,2%%time:~3,2%%time:~6,2%.log
set SOURCE_PATH_LIST=D:\BALBOA_SW\trunk\00_SW\00_SW_DEV, D:\BALBOA_SW\trunk\02_FPGA\01_K7

echo At %date% %time%, start to execute the svn update operation... >> %LOG_PATH_NAME%

for %%i in (%SOURCE_PATH_LIST%) do (
    cd /d %%i

	echo; >> %LOG_PATH_NAME%
	echo Enter %%i folder, execute the svn update operation... >> %LOG_PATH_NAME%

    svn cleanup .
    svn cleanup . --remove-unversioned --remove-ignored --non-interactive >> %LOG_PATH_NAME% 2>&1
    svn revert . --recursive  --non-interactive >> %LOG_PATH_NAME% 2>&1
    svn update >> %LOG_PATH_NAME% 2>&1
)

```



