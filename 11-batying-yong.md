

``` bash
@echo off

:a

ping -n 3 127.0.0.1&gt;nul

cmd /c time 12:35:00



ping 127.1 -n 5 &gt;nul

goto :a
``` 

