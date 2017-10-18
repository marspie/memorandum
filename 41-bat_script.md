1.bat 修改系统时间

```bash
@echo off

:a

ping -n 3 127.0.0.1&gt;nul

cmd /c time 12:35:00

ping 127.1 -n 5 &gt;nul

goto :a
```

2.bat 守护进程

```bash
@echo off

set _task=pis_server.exe
set _svr=D:\PIS\ground_pis_server\pis_server.exe
set _des=start.bat

:checkstart
for /f "tokens=5" %%n in ('qprocess.exe ^| find "%_task%" ') do (
 if %%n==%_task% (goto checkag) else goto startsvr
)



:startsvr
echo %time% 
echo ********程序开始启动********
echo 程序重新启动于 %time% ,请检查系统日志 >> restart_service.txt
echo start %_svr% > %_des%
echo exit >> %_des%
start %_des%
set/p=.<nul
for /L %%i in (1 1 10) do set /p a=.<nul&ping.exe /n 2 127.0.0.1>nul
echo .
echo Wscript.Sleep WScript.Arguments(0) >%tmp%\delay.vbs 
cscript //b //nologo %tmp%\delay.vbs 10000 
del %_des% /Q
echo ********程序启动完成********
goto checkstart


:checkag
echo %time% 程序运行正常,10秒后继续检查.. 
echo Wscript.Sleep WScript.Arguments(0) >%tmp%\delay.vbs 
cscript //b //nologo %tmp%\delay.vbs 10000 
goto checkstart
```

3.bat kill进程

```bash
taskkill /F /IM pis_server.exe
```

4.bat 合并文件，修改文件编码

```
@echo off
set "指定文件=ground_pids_database.sql"
echo 开始合并SQL ...
echo create_db.sql
type create_db.sql > temp.sql
echo create_table.sql
type create_table.sql >>temp.sql
cd MYSQL
type *.sql >> ../init_all.sql
cd ..
echo.
type init_all.sql >>temp.sql
echo create_procedure.sql
type create_procedure.sql >>temp.sql
echo.
iconv.exe -f GBK -t UTF-8 temp.sql > %指定文件%
echo 合并完成.
del init_all.sql
del temp.sql
pause
```



