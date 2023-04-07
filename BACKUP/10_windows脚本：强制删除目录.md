# [windows脚本：强制删除目录](https://github.com/cutepig123/gitblog/issues/10)

```
SET DIRECTORY_NAME=%~1
TAKEOWN /f "%DIRECTORY_NAME%" /r /d y
ICACLS "%DIRECTORY_NAME%" /grant administrators:F /t
ICACLS "%DIRECTORY_NAME%" /reset /T
echo We will delete the folder "%DIRECTORY_NAME%"
PAUSE
rd/s/q "%DIRECTORY_NAME%"


```
