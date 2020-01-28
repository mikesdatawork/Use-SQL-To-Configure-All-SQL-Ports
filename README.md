![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Use SQL To Configure All SQL Ports
**Post Date: June 24, 2014**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Some people feel the only option for setting the ports is from the server directly. You don't need to literally logon to the Windows Server where SQL Server resides in order to set the port. You can use SSMS as usual provided you have an account that has admin rights on the Windows Server where SQL is installed.
If you do; simply run this:</p>      


## SQL-Logic
```SQL
use master;
set nocount on
exec sp_configure 'show advanced options', '1'; reconfigure
exec sp_configure 'xp_cmdshell', '1'; reconfigure
go
 
exec master..xp_cmdshell
'@echo SETTING ALL STANDARD SQL PORTS
@echo SQL SERVICE PORTS 1433
netsh advfirewall firewall add rule name="SQL Server" dir=in action=allow protocol=TCP localport=1433 @echo DEDICATED ADMIN PORTS 1434
netsh advfirewall firewall add rule name="SQL Admin Connection" dir=in action=allow protocol=TCP localport=1434 @echo SERVICE BROKER PORTS
netsh advfirewall firewall add rule name="SQL Service Broker" dir=in action=allow protocol=TCP localport=4022 @echo TSQL/RPC port 135
netsh advfirewall firewall add rule name="SQL Debugger/RPC" dir=in action=allow protocol=TCP localport=135 @echo SSAS PORTS
netsh advfirewall firewall add rule name="Analysis Services" dir=in action=allow protocol=TCP localport=2383 @echo Enabling SQL Server Browser Service port 2382
netsh advfirewall firewall add rule name="SQL Browser" dir=in action=allow protocol=TCP localport=2382 @echo SETTING STANDARD APP PORTS IF ANY
@echo HTTP port 80
netsh advfirewall firewall add rule name="HTTP" dir=in action=allow protocol=TCP localport=80 @echo HTTP port 25
netsh advfirewall firewall add rule name="SMTP" dir=in action=allow protocol=TCP localport=25 @echo SSL port 443
netsh advfirewall firewall add rule name="SSL" dir=in action=allow protocol=TCP localport=443 @echo SQL BROWSER PORTS
netsh advfirewall firewall add rule name="SQL Browser" dir=in action=allow protocol=UDP localport=1434 @echo MULTICAST UDP PORTS
netsh firewall set multicastbroadcastresponse ENABLE'
```
Hope this is useful. 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

    
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

