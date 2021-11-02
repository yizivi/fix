Takeown
takeown /F M:\windows\ /a /r /d y & icacls M:\windows\  /T /C /grant users:(F,WDAC) /inheritance:e

mklink
mklink /J "C:\Users\Administrator\AppData\Roaming\Apple Computer\MobileSync" "E:\Program Files\iTunesMedia\MobileSync"

chrome group
删除注册表\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome 下对应的文件夹：EnabledPlugins 浏览器地址栏输入 chrome://flags/#show-managed-ui ( 选项是否启用, 其应为 Disabled )，并重启浏览器

Dism
dism /image:c:\ /get-packages /format:table dism /image:c:\ /remove-package /packagename:Package_for_KB283414031bf3856ad364e35amd64~~6.1.2.0 

dism /online /get-packages dism /online /remove-package /packagename:Package_for_KB451665531bf3856ad364e35amd64~~6.1.1.1

Wusa
wusa.exe /uninstall /kb:4516655

批量解锁

dsquery user  -limit 0 "OU=U1city,DC=U1city,DC=net" | dsmod user -Disabled no

删除计划任务

schtasks /delete /TN Rass /F

修复升级windows时提示：我们无法告知你的电脑是否有足够的空间来继续安装

reagentc /disable  reagentc /setreimage /path \?\GLOBALROOT\device\harddisk0\partition4\Recovery\WindowsRE

reagentc /enable

无法启动到恢复环境，修复bcdedit /enum提示无法打开启动配置存储

启动到修复环境

bootrec /rebuildbcd

修复WMI

@echo on  cd /d c:\temp if not exist %windir%\system32\wbem goto TryInstall cd /d %windir%\system32\wbem net stop winmgmt winmgmt /kill if exist Rep_bak rd Rep_bak /s /q rename Repository Rep_bak for %%i in (.dll) do RegSvr32 -s %%i for %%i in (.exe) do call :FixSrv %%i for %%i in (.mof,.mfl) do Mofcomp %%i net start winmgmt goto End

:FixSrv if /I (%1) == (wbemcntl.exe) goto SkipSrv if /I (%1) == (wbemtest.exe) goto SkipSrv if /I (%1) == (mofcomp.exe) goto SkipSrv %1 /RegServer

:SkipSrv goto End

:TryInstall if not exist wmicore.exe goto End wmicore /s net start winmgmt :End --------------------- 
